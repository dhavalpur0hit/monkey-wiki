# Securing networks together
Want to help secure networks? That's great! However, it's never that simple.

Here's a few short links to help you get started.

* [Getting up and running](https://github.com/guardicore/monkey/wiki/Getting-up-and-running) - To help you get a working development setup
* [Contributing guidelines](https://github.com/guardicore/monkey/blob/master/CONTRIBUTING.md) - Some guidelines to help you submit

# What are we looking for?
* More exploits! The best way to find weak spots in the network is by attacking it. The [Exploit template](https://github.com/guardicore/monkey/wiki/Exploit-templates) page will help you add exploits. 
It's important to note that the Infection Monkey must be perfectly reliable otherwise no one will use it, so avoid memory corruption exploits _unless they're rock solid_ and focus on the logical stuff such as Shellshock.

* Analysis plugins - Successfully attacking every server in the network is no good unless the Monkey can explain how to prevent the attack. Whether it's detecting when the Monkey is using stolen credentials or when the Monkey can escape locked down networks, this is the part that actually helps secure different parts.

* Better framework code - We always want to improve the core Monkey code, to make it smaller, faster and more reliable. If you have an idea of how to do it, or just want to modularise the code, do share!

# Documentation
Every project requires better documentation. The Monkey is no different, so feel free to open PRs with suggestions, improvements or issues asking us to document different parts of the Monkey.


