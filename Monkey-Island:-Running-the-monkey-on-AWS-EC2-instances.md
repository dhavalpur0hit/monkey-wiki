# When to use this feature
If your network is deployed on Amazon Web Services (with EC2 instances), and you'd like to run the Infection Monkey in order to test it. You can easily run the monkey on **various instances** within your network - in a secure fashion, without feeding the Island with any credentials or running shell commands on the machines you want to test.

![AWS logo](https://www.securview.com/wp-content/uploads/2018/02/aws-logo.png)

# Setup
Assuming your network is already set up in AWS EC2, follow these quick steps to get up and running.

## Monkey Island deployment
In order to run the Monkeys directly from the Monkey Island server, you need to deploy the Monkey Island server to an AWS EC2 instance in the same network which you want to test. For information about deploying the Monkey Island server, see [setup documentation](https://github.com/guardicore/monkey/wiki/setup).

## Setup IAM roles
In order for the Island to successfully view your instances, you'll need to set appropriate IAM roles to your instances. You can read more about IAM roles [in Amazon's documentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html), but it's not necessary in order to follow this setup.

### Creating a custom IAM role
Go to the [AWS IAM roles dashboard](https://console.aws.amazon.com/iam/home?#/roles) and create a new IAM role for EC2, with the `AmazonEC2RoleforSSM` permission. In the end it should like something like this:

[[images/monkey-island-aws-screenshot-3.png]]

### Applying the IAM role to an instance
For each instance you'd like to access from the island, apply the new IAM role you've just created to the instance. For example: 

[[images/monkey-island-aws-screenshot-4.png]]

# Usage
When you run the monkey island on an AWS instance, the island detects it's running on AWS and present the following option in the _"Run Monkey"_ page, like so:

[[images/monkey-island-aws-screenshot-1.png]]

And then you can choose one of the available instances as "patient zero" like so:

1. Click on "Run on AWS"
2. Choose the relevant Network Interface
3. Select the machines you'd like to run the Monkey on
4. Click "Run on Selected Machines", and watch the monkey go! 🐒 

[[images/monkey-island-aws-screenshot-2.png]]
