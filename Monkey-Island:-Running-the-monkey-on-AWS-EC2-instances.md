# When to use this feature
If your network is deployed on Amazon Web Services (with EC2 instances), you can easily run the monkey on various instances in your network for testing - in a secure fashion, without feeding the Island with any credentials or running shell commands on the machines you want to test.

![AWS logo](https://commons.wikimedia.org/wiki/File:Amazon_Web_Services_Logo.svg)

# How does it look
When you run the monkey island on an AWS instance, the island detects it's running on AWS and present the following option in the _"Run Monkey"_ page, like so:


# Setup
Assuming your network is already set up in AWS EC2, follow these quick-n-easy steps and get to run the testing!

## Monkey Island deployment
In order to run the Monkeys directly from the Monkey Island server, you need to deploy the Monkey Island server to an AWS EC2 instance in the same network which you want to test. For information about deploying the Monkey Island server, see [https://github.com/guardicore/monkey/wiki/setup](our setup documentation).

## IAM 