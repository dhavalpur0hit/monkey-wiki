# PassTheHash



## Changes to MongoDB

We store the information gathered from the machine using WMI queries and Mimikatz output in a new collection called "UsersAndGroups".
Each document in the collection will include these fields:

- type [int]: 1 for documents representing users and 2 for groups.
- SID [string]: is a unique value of variable length used to identify a trustee. Each account has a unique SID issued by an authority, such as a Windows domain controller, and stored in a security database. 
- name [string]: The display name of the group or user.
- domain_name [string]: The displayed domain name of the group or user.
- machine_id [ObjectId]: If the account (user or group) is a local account, than we document the monkey's ID of the account's machine.
- member_of [Array of SID]: Which groups does this account belongs to.
- admin_on_machines [Array of machine_id]: on which machine this account is an admin (part of the Administrators group)

In case the account is a type 1 account (user), we add these fields to the document:
    
- NTLM_secret [string]: NTLM credentials found in the SAM using Mimikatz.
- SAM_secret [string]: Cached credentials found in the SAM using Mimikatz.
- secrets_location [ObjectId]: On what machine (monkey_id) the secrets were found.

And in case it's a type 2 account (group), we add this field:

- entities_list [Array of SID]: A list of users or groups that are members of the group.
    
There are also changes to an existing collection - 'monkey':
    
we're adding this field:
- critical_services [Array of strings]: States if there are any predefined services installed on the machine i.e MSSQL, DC, DNS, etc...
  
## Data Sources

The data gathered from the machine is being sent to the island by the monkey in the shape of a 'system_info' telemetry request. This request holds the Mimikatz and WMI output from the machine with other information gathered by the monkey, and using that information the Monkey Island creates a document for each user and group found on the machine using the fields mentioned above.
The connections between users and groups on the machine is being created using mostly 3 WMI classes:
 - Win32_GroupUser - a list of (Group, Group\User) pairs for each profile on the machine, i.e ('Administrators', 'MyAdmin').
 - Win32_Group - A list of all of the windows groups saved on the machine.
 - Win32_UserAccount - A list of all of the windows users saved on the machine.
 
The critical services classification is being done using this WMI class:
- Win32_Service - a list of all installed services on the machine.

## Monkey Island Data Ingestion Pipeline 

The data processing happens at the stage of 'system_info_collection' telemetry processing and is applied per machine, 

1.  Create a list of dictionaries for all the users gathered
2.  Create a list of dictionaries for all the groups gathered
3.  Iterate over the GroupUser WMI class to find which user or group is a member of what group.
4.  Push all the users and groups info to the mongo

There's a chance for each domain group or user that it was already found on another machine in the domain and a mongo doc is already created for it, therefore we need to take it into account and use updates and not flat inserts.

After the data is processed and inserted to the DB, The users and groups that are members of the 'Administrators' group that was fetched from the processed machine are being registered as admins of that machine by adding the machine_id to each user or group 'admin_on_machines' field.

    def add_admin(group, machine_id):
		for entity in group:
			entity.admin_on_machines += machine_id
			if entity is group:
				add_admin(entity, machine_id)
	
	#The call is:
	add_admin(local_admins_group, machine_id)

Next stage is to check for each user if the groups that it's a member of, are admin groups in one or more of all the machines collected so far.
Meaning, if group G is admin on machine X we update user U that is a member of G that U is an admin on machine X in case the user doesn't already have machine X in its list.

    For user in collected_users:
		for group in user.member_of: # the group details is fetched from the DB using the group's SID from the 'member_of' list.
			db.update(user.admin_on_machines $addToSet: group.admin_on_machines) #Pseudo code

## Report Generation

3 queries needs to be used, one for each situation:

1. Shared local admin
        In this one we decided to exclude 'Administrator' named users, its a false positive since it makes sense for a user
        named 'Administrator' to apear on multiple machines.

        db.getCollection('groupsandusers').find({'type': USERTYPE, 'name': {'$ne': 'Administrator'},
                                               'admin_on_machines.1': {'$exists': True}},
                                              {'admin_on_machines': 1, 'name': 1, 'domain_name': 1})

2. Shared users passwords
    
        db.groupsandusers.aggregate([
        {"$match": {
                'NTLM_secret': {
                    "$exists": "true", "$ne": None}
            }},
            {
                "$group": {
                    "_id": {
                        "NTLM_secret": "$NTLM_secret"},
                    "count": {"$sum": 1},
                    "Docs": {"$push": {'_id': "$_id", 'name': '$name', 'domain_name': '$domain_name',
                                       'machine_id': '$machine_id'}}
                }},
            {'$match': {'count': {'$gt': 1}}}
        ])

3. Strong users on critical machines

        db.getCollection('groupsandusers').aggregate([
        {
                '$unwind': '$admin_on_machines'
            },
            {
                '$match': {'type': USERTYPE, 'domain_name': {'$ne': None}}
            },
            {
                '$lookup':
                    {
                        'from': 'monkey',
                        'localField': 'admin_on_machines',
                        'foreignField': '_id',
                        'as': 'critical_machine'
                    }
            },
            {
                '$match': {'critical_machine.critical_services': {'$ne': []}}
            },
            {
                '$unwind': '$critical_machine'
            }
        
        ])

The queries produces data structured as close as it can be to the data required for the monkey report generation, this optimization reduced the report generation time by about 80% from ~15 seconds to ~3.