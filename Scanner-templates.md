The Infection Monkey agent has two steps before attempting to exploit a victim, scanning and fingerprinting, it's possible to customize both steps in the configuration files.

# Scanning
Currently there are two scanners, `PingScanner` and `TcpScanner` both inheriting from `HostScanner`. 

The sole interface required is the `is_host_alive` interface, which needs to return True/False. 

`TcpScanner` is the default scanner and it checks for open ports based on the `tcp_target_ports` configuration setting. 

`PingScanner` sends a ping message using the host OS utility `ping`.


# Fingerprinting
Fingerprinters are modules that collect server information from a specific victim. They inherit from the `HostFinger` class and are listed under `finger_classes` configuration option.

Currently implemented Fingerprint modules are 
1. `SMBFinger` - Fingerprints target machines over SMB. Extracts computer name and OS version.
2. `SSHFinger` - Fingerprints target machines over SSH (port 22). Extracts the computer version and SSH banner.
3. `PingScanner` - Fingerprints using the machines TTL, to differentiate between Linux and Windows hosts.
4. `HTTPFinger` - Fingerprints over HTTP/HTTPS, using the ports listed in HTTP_PORTS in the configuration. Returns the server type and if it supports SSL.
5. `MySQLFinger` - Fingerprints over MySQL (port 3306). Extracts MySQL banner info - Version, Major/Minor/Build and capabilities.
6. `ElasticFinger` - Fingerprints over ElasticSearch (port 9200). Extracts the cluster name, node name and node version.


# Adding a scanner/fingerprinter
To add a new scanner/fingerprinter, create a new class that inherits from `HostScanner` or `HostFinger` (depending on the interface). The class should be under the network module and should be imported under [network\__init__.py](https://github.com/guardicore/monkey/blob/master/chaos_monkey/network/__init__.py).

To be used by default, two files need to be changed - [config.py](https://github.com/guardicore/monkey/blob/master/chaos_monkey/config.py) and [example.conf](https://github.com/guardicore/monkey/blob/master/chaos_monkey/example.conf) to add references to the new class. 

At this point, the Monkey knows how to use the new scanner/fingerprinter but to make it easy to use, the UI needs to be updated. The relevant UI file is [config.py](https://github.com/guardicore/monkey/blob/master/monkey_island/cc/services/config.py) (not to be confused with the prior config.py)

