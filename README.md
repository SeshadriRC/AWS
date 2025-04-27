# AWS

**I AM Service**

1. What is IAM users,policies,groups and roles in AWS

Term | Meaning | Example

User | A person or app that logs in to AWS. | You (as a DBA), Jenkins server, etc.

Group | A collection of IAM users. You attach permissions once to the group, and all users inside get it. | "DBA-Team" group, "DevOps" group.

Policy | A set of permissions written in JSON. You attach policies to Users, Groups, or Roles. | A policy that says: "Allow read access to S3 bucket."

Role | A temporary identity with permissions, assumed by users or AWS services. | EC2 instance assumes a role to access S3 without a password.

Quick Points:

Users = Login with username/password or access keys.

Groups = Help manage permissions in bulk.

Policies = Define what actions are allowed/denied.

Roles = No long-term credentials; used for services or cross-account access.
