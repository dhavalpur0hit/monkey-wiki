# What is this? 
The Infection Monkey integration with the [AWS Security Hub](https://aws.amazon.com/security-hub/) allows anyone to verify and test the resilience of their AWS environment and correlate this information with the native security solutions and benchmark score.

[[images/security_hub/security-hub-logo-ink.png]]

# Setup
If the correct permissions have been set on the AWS IAM role of the Monkey Island machine (see [IAM roles and Infection Monkey](https://github.com/guardicore/monkey/wiki/Monkey-Island:-Running-the-monkey-on-AWS-EC2-instances)), then the Island will automatically export its findings to the AWS security hub. 

## Specific permissions required for security hub
* `"securityhub:UpdateFindings"`
* `"securityhub:BatchImportFindings"`

Note that the integration is specifically between your Monkey Island and the security hub. The Infection Monkey is an free project and there is no centralised infrastructure.

# Integration details
The Infection Monkey reports the following types of issues to the AWS security hub
* Software and Configuration Checks/Vulnerabilities/CVE

Specifically, the Island sends findings for all vulnerabilities it finds along with generic findings on the network (such as segmentation issues).

Our normalized severity is 100, while most issues we report range between 1 and 10.

## Regions
The Infection Monkey is usable on all public AWS instances.

# Example
After setting up a monkey environment in AWS and attaching the correct IAM roles to the monkey island machine, the report findings were exported to the security hub.

1. Press `Findings`
2. Press on the specific finding to see more details and possible solutions. 
[[images/security_hub/security-hub-console-example.png]]
