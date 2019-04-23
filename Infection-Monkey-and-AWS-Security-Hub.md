# What is this? 
The infection monkey integration with the [AWS Security Hub](https://aws.amazon.com/security-hub/) allows anyone to verify and test the resilience of their AWS environment and correlate this information with the native security solutions and benchmark score.

If the correct permissions have been set on the AWS IAM role of the monkey island machine (see [IAM roles and Infection Monkey](https://github.com/guardicore/monkey/wiki/Monkey-Island:-Running-the-monkey-on-AWS-EC2-instances)), then the Island will automatically export its findings to the AWS security hub. 

For example:

[[images/security_hub/security-hub-console-example.png]]
