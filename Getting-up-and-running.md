Getting a working environment up and running for the Infection Monkey is very easy.


# Agent 
The Agent, termed the Monkey, is a single Python project under the Chaos Monkey folder. Built for Python 2.7, you can get up and running by setting up a [virtual environment](http://docs.python-guide.org/en/latest/dev/virtualenvs/) and inside it installing the requirements listed under [requirements.txt](https://github.com/guardicore/monkey/blob/master/chaos_monkey/requirements.txt).

In order to compile the Monkey for distribution by the Monkey Island, you need to run the instructions listed in the [readme.txt](https://github.com/guardicore/monkey/blob/master/chaos_monkey/readme.txt) on each supported env. 

This means setting up an env with Linux 32/64 bit with Python installed and a Windows 64 bit machine with developer tools + 32/64 bit python versions.

# Monkey Island
The Monkey Island is a Python backend React frontend project. Similar to the agent, the backend's requirements are listed in the matching [requirements.txt](https://github.com/guardicore/monkey/blob/master/monkey_island/requirements.txt). To setup a working front env, install the npm packages listed in the [package.json](https://github.com/guardicore/monkey/blob/master/monkey_island/cc/ui/package.json) file. 