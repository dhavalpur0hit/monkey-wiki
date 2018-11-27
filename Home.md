The Infection Monkey is an open source security tool for testing a data center's resiliency to perimeter breaches and internal server infection. The Monkey uses various methods to self propagate across a data center and reports success to a centralized Monkey Island Command and Control server.

The Infection Monkey is comprised of two parts:
* Monkey - A tool which infects other machines and propagates to them
* Monkey Island - A dedicated UI to visualize the Infection Monkey's progress inside the data center

To read more about the Monkey, visit [http://infectionmonkey.com](http://infectionmonkey.com)


Main Features
---------------

The Infection Monkey uses the following techniques and exploits to propagate to other machines.

* Multiple propagation techniques:
  * Predefined passwords
  * Common logical exploits
  * Password stealing using mimikatz
* Multiple exploit methods:
  * SSH
  * SMB
  * RDP
  * WMI
  * Shellshock
  * Conficker
  * SambaCry
  * Elastic Search (CVE-2015-1427)


Getting Started
---------------
Check out the [Setup](https://github.com/guardicore/monkey/wiki/setup) page or read a [quick walkthrough](https://www.guardicore.com/infectionmonkey/wt/).