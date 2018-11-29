Getting a working environment up and running for the Infection Monkey is very easy.

## Agent

The Agent, (what we refer as the Monkey), is a single Python project under the [`infection_monkey`](https://github.com/guardicore/monkey/blob/master/monkey/infection_monkey) folder. Built for Python 2.7, you can get it up and running by setting up a [virtual environment](https://docs.python-guide.org/dev/virtualenvs/) and inside it installing the requirements listed under [`requirements.txt`](https://github.com/guardicore/monkey/blob/master/monkey/infection_monkey/requirements.txt).

In order to compile the Monkey for distribution by the Monkey Island, you need to run the instructions listed in [`readme.txt`](https://github.com/guardicore/monkey/blob/master/monkey/infection_monkey/readme.txt) on each supported environment.

This means setting up an environment with Linux 32/64-bit with Python installed and a Windows 64-bit machine with developer tools + 32/64-bit Python versions.

## Monkey Island

The Monkey Island is a Python backend React frontend project. Similar to the agent, the backend's requirements are listed in the matching [`requirements.txt`](https://github.com/guardicore/monkey/blob/master/monkey/monkey_island/requirements.txt).

To setup a working front environment, run the instructions listed in the [`readme.txt`](https://github.com/guardicore/monkey/blob/master/monkey/monkey_island/readme.txt)