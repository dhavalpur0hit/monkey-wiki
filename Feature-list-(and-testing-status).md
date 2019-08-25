# Exploiters

| Feature 	| How is it tested 	| Notes 	|
|---------	|------------------	|-------	|
| SSH user password	| Monkey Zoo | SSH.conf |
| SSH keypair	| Monkey Zoo | SSH.conf |
| WMI user password | Monkey Zoo | WMI_MIMIKATZ.conf |
| WMI PTH	| Monkey Zoo | WMI_MIMIKATZ.conf |
| SMB user password	| Monkey Zoo | SMB_MIMIKATZ.conf |
| SMB PTH	| Monkey Zoo | SMB_MIMIKATZ.conf |
| Sambacry	| Monkey Zoo | |
| ElasticGroovy	| Monkey Zoo | |
| OracleWebLogic	| Monkey Zoo | |
| Struts2	| Monkey Zoo | |
| Hadoop yarn	| Monkey Zoo | |
| mssql	| Monkey Zoo | |
| shellshock - apache CGI	| Monkey Zoo | |
| rdp | Not tested | |
| conficker	| Not tested | |

# Other Agent Features

| Feature 	| How is it tested 	| Notes 	|
|---------	|------------------	|-------	|
| Tunneling TCP	| Monkey Zoo | |
| Tunneling HTTP	| Monkey Zoo | |
| SSH key-stealing	| Monkey Zoo | SSH.conf |
| Mimikatz (Windows password hash stealing)	| Monkey Zoo | SMB_MIMIKATZ.conf or WMI_MIMIKATZ.conf |
| Process list windows	| NOT TESTING | |
| Process list linux	| NOT TESTING | | 
| Local network interface windows	| NOT TESTING | | 
| Local network interface linux	| NOT TESTING | | 
| Azure guest agent password stealing	| NOT TESTING | | 
| Windows service discovery	| NOT TESTING | | 
| Post breach actions	| Monkey Zoo | |
| Upgrade windows agent to 64bit	| Monkey Zoo | Some blind exploiter, we need to add the ability to build 32-bit monkey in island |

# Island features

| Feature 	| How is it tested 	| Notes 	|
|---------	|------------------	|-------	|
| Segmentation | Monkey Zoo | |
| AWS detection	| NOT TESTING | |
| AWS listing	| NOT TESTING | |
| AWS sec hub	| NOT TESTING | |
| Per machine, recommendations generated | Monkey Zoo | |
| Tunneling map - edge of tunneling created	| Monkey Zoo | |
| Test status of each directive | Monkey Zoo | Zero Trust |
| Test number of findings	| Monkey Zoo | Zero Trust |