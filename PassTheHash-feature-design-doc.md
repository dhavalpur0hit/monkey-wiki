# PassTheHash

## Where does the info come from
Right now we use 2 sources of information gathering
   - Mimikatz output for secrets per user
   - WMI classes for Users and Groups info

## How do we order the information
There's a new mongoDB collection called "Entities" that will represent users and groups information as described bellow
### Shared info between users and groups (base entity)
 - SID
 - Name
 - Domain name (if relevant)
 - machine_id (ObjectId of the relevant monkey this info was gathered with)
 - admin_on_machines (on which machines this entity have administrative rights)

### Users specific info
 - Secrets* (all kinds of secrets gathered)
 - machines_secrets_found_on (Where did the monkey found the secrets on)

### Groups specific info
  - entities_list ( a unique list of entities that are members of this group, either users or groups)

### Changes to the current monkey collection
  - critical_services ( a list of services installed that we've decided are critical)
  - isDC (a flag to signal if this machine is a DC or not)

## How do we use the info gathered
from the sources i've mantioned above we create the entities and then we update the groups and users documents on the run with gathered information about admin rights on machines or relations to groups.

after the described run is finished we go over the Administrators group and recursively update for each entry in the group the relevant users affected by the recently found admins (users or groups).

## From Python to MongoDB

Because we have to lock the DB for the transaction to happen (to stop other information coming from different monkeys interfere with already gatherd info), we decided to orgenize the whole information gathered in a pythonic data stracture and bulk-update the collection while keeping the DB lock time to minimum.

## From MongoDB to the Report

This way of orgenizing the information gathered in the mongoDB will help create the monkey's report by making all of the relevant information available in report-friendly way so only a couple of mongo queries are required to use the information for the report. The queries will be written soon as we'll settle on the propper DB design.