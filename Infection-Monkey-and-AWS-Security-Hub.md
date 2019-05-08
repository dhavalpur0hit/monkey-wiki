# What is this? 
The infection monkey integration with the [AWS Security Hub](https://aws.amazon.com/security-hub/) allows anyone to verify and test the resilience of their AWS environment and correlate this information with the native security solutions and benchmark score.

[[images/security_hub/security-hub-logo-ink.png]]

# Setup
If the correct permissions have been set on the AWS IAM role of the monkey island machine (see [IAM roles and Infection Monkey](https://github.com/guardicore/monkey/wiki/Monkey-Island:-Running-the-monkey-on-AWS-EC2-instances)), then the Island will automatically export its findings to the AWS security hub. 

# Example
After setting up a monkey environment in AWS and attaching the correct IAM roles to the monkey island machine, the report findings were exported to the security hub.

1. Press `Findings`
2. Press on the specific finding to see more details and possible solutions. 
[[images/security_hub/security-hub-console-example.png]]
