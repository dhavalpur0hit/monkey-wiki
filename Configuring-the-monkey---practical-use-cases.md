This page aims to explain and demonstrate useful Monkey configuration use cases. 

![Settings icon](https://image.flaticon.com/icons/png/128/219/219525.png)

# Required setup
After setting up the monkey island (see [setup](https://github.com/guardicore/monkey/wiki/Setup)) but **before** running the monkey, you can configure the monkey to change it's behavior, in this menu: 

[[images/MonkeyIslandMenu_Configuration.png]]

You can also run the monkey manually and provide it with a configuration file via the command-line.

# Use cases
## Add brute-force usernames and passwords
To make sure you see the monkey propagating through your network, or to simulate a "phishing" attack or a password leak from your organization, you can add to the monkey's configuration usernames and passwords. The monkey will try to use these usernames and passwords to move through your network. 
