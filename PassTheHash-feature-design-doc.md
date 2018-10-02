# PassTheHash



## Changes to MongoDB

We store the information gathered from the machine using WMI queries and Mimikatz output in a new collection called "Profiles".
Each document in the collection will include these fields:

- type: 1 for documents representing users and 2 for groups.
- SID: is a unique value of variable length used to identify a trustee. Each account has a unique SID issued by an authority, such as a Windows domain controller, and stored in a security database.
- name: The display name of the group or user.
- domain_name: The displayed domain name of the group or user.
- machine_id: If the account (user or group) is a local account, than we document the monkey's ID of the account's machine.
- member_of: Which groups does this account belongs to.
- admin_on_machines: on which machine this account is an admin (part of the Administrators group)

In case the account is a type 1 account (user), we add these fields to the document:
    
- NTLM_secret: NTLM credentials found in the SAM using Mimikatz.
- SAM_secret: Cached credentials found in the SAM using Mimikatz.
- secrets_location: On what machine (monkey_id) the secrets were found.

And in case it's a type 2 account (group), we add this field:

- entities_list: A list of accounts that are part of the group.
    
There are also changes to an existing collection - 'monkey':
    
we're adding these fields:
- critical_services: States if there are any pre-defind services installed on the machine i.e MSSQL, DC, DNS, etc...
- isDC: True if the machine is a DC, this will allow for better future analysis of DC only information.
  
## What data is used

The data gathered from the machine is being sent to the island by the monkey in the shape of a 'system_info' telemetry request. This request holds the MiMikatz and WMI output from the machine with other information gathered by the monkey, and using that information the Monkey Island creates a document for each user and group found on the machine using the fields mentioned above.
The connections between users and groups on the machine is being created using mostly 3 WMI classes:
 - Win32_GroupUser - a list of (Group, Group\User) pairs for each profile on the machine, i.e ('Administrators', 'MyAdmin').
 - Win32_Group - A list of all of the windows groups saved on the machine.
 - Win32_UserAccount - A list of all of the windows users saved on the machine.
 
The critical services classification is being done using this WMI class:
- Win32_Service - a list of all installed services on the machine.

## Data Digestion

The data processing happens at the stage of 'system_info_collection' telemetry processing, 

1.  create a list of dictionaries for all the users gathered
2.  create a list of dictionaries for all the groups gathered
3.  create a groups hierarchy tree stating which user or group is included in what group.
4.  push all the users and groups info to the mongo

After the data is processed and inserted to the DB, the 'Administrators' groups and the machine id of which the group found on are fetched from the DB and for each entity (user\group) in the group the machine id is being added to its 'admin_on_machines' list.

    def add_admin(group, machine_id):
		for entity in group:
			entity.admin_on_machines += machine_id
			if entity is group:
				add_admin(entity, machine_id)
	
	#The call is:
	add_admin(local_admins_group, machine_id)

After this retroactive update happens, for each user we add its parent-group's 'admin_on_machines' list to its own.

    for user in collected_users:
		for group in user.member_of: # the group details is fetched from the DB using the group's SID from the 'member_of' list.
			user.admin_on_machines += group.admin_on_machines

all of the updates are being pushed to the DB at the end of this process.

## Report Generation

3 queries needs to be used, one for each situation:

1. Shared local admin
2. Shared admin passwords
3. Strong users on critical machines

The queries are still in the process of being finished and optimized.

The queries are expected to return data structured as close as it can be to the data the report generation pipeline expects to get, requiring as little as possible processing thus making the whole generation process a lot faster and optimized.