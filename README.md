# AWS

## Topics
[I AM Service](#i-am-service)

[EC2](#ec2)

## I AM Service

![image](https://github.com/user-attachments/assets/e6f11697-a64c-4ddf-bbf8-542be73daeed)
![image](https://github.com/user-attachments/assets/1c6e0d70-d375-490b-8e63-e7f35bcde540)
![image](https://github.com/user-attachments/assets/4dba025a-f30e-4e9c-8363-1f9cc777c30c)


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

**How to create a user in IAM**

2. Create User:
   
In the IAM dashboard, click Users (left side).

Click Add Users (top-right).

3. Set User Details:
   
Enter a User Name (example: dbadmin).

Select Access Type:

Password (for Console access) → If the user needs to log in to AWS website.

Access Key (for Programmatic access) → If the user will access AWS via CLI, API, SDK.

(You can select both if needed.)

4. Set Permissions:
   
You get 3 options:

Add to Group (recommended if you already have groups with permissions).

Copy permissions from existing user.

Attach policies directly (like AdministratorAccess, AmazonS3ReadOnlyAccess, etc).

Choose one based on what you want.

5. (Optional) Set Tags:
   
You can add tags like Key: Department, Value: DBA.

7. Review and Create:
   
Review all settings.

Click Create User.

After Creation:

If you enabled console access, a temporary password is generated — give it to the user.

If programmatic access is selected, an Access Key ID and Secret Access Key are generated — download them securely.

**How to create a group in IAM**

1. Go to IAM:
   
Login to AWS Console.

Open IAM service.

2. Go to Groups:
   
In the left menu, click User groups.

4. Choose the Group:
   
Click the Group name where you want to add users.

5. Add Users:
   
Inside the group, click the "Add users" button (top-right).

Select the users you want to add (checkbox).

Click Add users at the bottom.

**How to create a policy in IAM**

1. Go to IAM:
   
Login to AWS Console.

Open IAM.

2. Open Policies:
   
On the left side, click Policies.

4. Create Policy:
   
Click Create policy (top-right).

6. Set Permissions:
   
You have two options:

Visual Editor → You can select Service, Actions, Resources easily (no coding).

JSON → You can paste/write your own JSON policy.

Example (Visual Editor way):

Choose Service (example: S3).

Choose Actions (example: ListBucket and GetObject).

Choose Resources (example: Specific bucket or all buckets).

Example (JSON way):

json
Copy
Edit
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "s3:ListBucket",
            "Resource": "arn:aws:s3:::example-bucket"
        }
    ]
}

5. Add Tags (optional):

You can tag it if you want (not mandatory).

6. Name and Create:
   
Give a Policy Name (example: S3ReadOnlyPolicy).

(Optional) Add a description.

Click Create policy.

## EC2
