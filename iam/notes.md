# Notes

## What does IAM provide

- centralized control of the AWS account
- identity federation with active directory, and other OAuth providers
- multifactor authentication and allows temporary access
    - temporarily get data from S3 buckets for example
- password rotation policies
- supports PCI DSS compliance

## Key Exam Terms

- Users - means end users (think people using the service, not developers)
- Groups - a collection of users under a single set of permissions
- Roles - you can create roles and assign them to AWS resources (think AWS resources, not people)
    - for example, a role can be granted to an EC2 instance to allow it to do something, like read from an S3 bucket
- Policies - a document that defines one or more permissions, which can be attached to an IAM entity (such as a user, group, or role)
    - a policy can be likened to an active directory GPO/Group Policy Object
    - a policy document is represented in `json` or `yaml` in AWS

## Summary

- IAM is universal - meaning it always applies to the entire account, not regions
- You should never do anything with the *root* account. Always make IAM user accounts, give those permissions, and use those instead
- New users have *no* permissions when first created. This is by design
- Always setup MFA on the root account, as well as password rotation policies for IAM users


## Questions

- What is CloudHSM?
- How do I define and assign a temporary access IAM role?