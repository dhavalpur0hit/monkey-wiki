# What's this?

Before each release, we'd like to test the following features to make sure we're passing a high-quality bar.

## Feature tests

### Monkey Agent

#### Exploiters

| Feature 	| How is it tested 	| Notes 	|
|---------	|------------------	|-------	|
| SSH user password	| Monkey Zoo | SSH.conf, TUNNELING.conf |
| SSH keypair	| Monkey Zoo | SSH.conf |
| WMI user password | Monkey Zoo | WMI_MIMIKATZ.conf |
| WMI PTH	| Monkey Zoo | WMI_MIMIKATZ.conf |
| SMB user password	| Monkey Zoo | SMB_MIMIKATZ.conf |
| SMB PTH	| Monkey Zoo | SMB_MIMIKATZ.conf |
| Sambacry	| UNKNOWN | |
| ElasticGroovy	| Monkey Zoo | ELASTIC.conf |
| OracleWebLogic	| Monkey Zoo | WEBLOGIC.conf |
| Struts2	| Monkey Zoo | STRUTS2.conf |
| Hadoop yarn	| Monkey Zoo | HADOOP.conf|
| MSSQL	| Monkey Zoo | MSSQL.conf (test didn't pass has a bug) |
| shellshock - apache CGI	| Monkey Zoo | SHELLSHOCK.conf |
| Conficker	| Not tested | |

#### System Info Collectors

| Feature 	| How is it tested 	| Notes 	|
|---------	|------------------	|-------	|
| Process list windows	| NOT TESTING | |
| Process list Linux	| NOT TESTING | | 
| Local network interface windows	| NOT TESTING | | 
| Local network interface Linux	| NOT TESTING | | 
| Azure guest agent password-stealing	| NOT TESTING | | 
| Windows service discovery	| NOT TESTING | | 
| Environment (Cloud vs On Prem)	| NOT TESTING | | 

#### Other Agent Features

| Feature 	| How is it tested 	| Notes 	|
|---------	|------------------	|-------	|
| Tunneling TCP	| Monkey Zoo | TUNNELING.conf |
| Tunneling HTTP	| Monkey Zoo | TUNNELING.conf |
| SSH key-stealing	| Monkey Zoo | SSH.conf |
| Mimikatz (Windows password hash stealing)	| Monkey Zoo | SMB_MIMIKATZ.conf or WMI_MIMIKATZ.conf |
| Post-breach actions	| Monkey Zoo | |
| Upgrade windows agent to 64bit	| Monkey Zoo | Some blind exploiter, we need to add the ability to build 32-bit monkey in island |

### Island features

| Feature 	| How is it tested 	| Notes 	|
|---------	|------------------	|-------	|
| Reporting | Monkey Zoo (manual) | |
| Segmentation | Monkey Zoo (manual) | |
| AWS detection	| NOT TESTING | |
| AWS listing	| NOT TESTING | |
| AWS sec hub	| NOT TESTING | |
| Per machine, recommendations generated | Monkey Zoo (manual) | |
| Tunneling map - edge of tunnelling created	| Monkey Zoo (manual) | |
| Test status of each directive | Monkey Zoo | NOT TESTING |
| Test number of findings	| Monkey Zoo | NOT TESTING |

## Deployment tests

| Feature 	| How is it tested 	| Notes 	|
|---------	|------------------	|-------	|
| Deploy Debian | Manually | Should be tested by 2 different people |
| Deploy Windows | Manually | Should be tested by 2 different people |
| Deploy VMWare	| Manually | Should be tested by 2 different people|
| Deploy Docker	| Manually | Should be tested by 2 different people |
| Deployment script Windows	| NOT TESTING | |
| Deployment script Linux	| NOT TESTING | |

## Stress tests

| Feature 	| How is it tested 	| Notes 	|
|---------	|------------------	|-------	|
| Full mesh network, 10 machines | Manually | All reports should load in under 3 seconds |
| 3 sub-networks, 10 machines | Manually | All reports should load in under 3 seconds |
| 3 users on the Island and 3 Monkeys simultaneously | Manually | Island should be responsive |
