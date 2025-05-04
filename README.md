# AWS

## Topics
[I AM Service](#i-am-service)

[EC2](#ec2)

- [Connect to EC2](#connect-to-ec2)

[VPC](#vpc)

[Firwall](#firewall)

[Security Group and NACL](#securitygroup-and-nacl)


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

![image](https://github.com/user-attachments/assets/ab70a543-bcdf-4bfc-9a44-fa044b4736c0)
![image](https://github.com/user-attachments/assets/bd86809b-5455-44b6-850e-829310bb4b6e)
![image](https://github.com/user-attachments/assets/bfc073c9-2fff-4f68-a4ed-da7a0228a213)
![image](https://github.com/user-attachments/assets/007b41c9-038e-4918-a36a-162f2b7fca1e)
![image](https://github.com/user-attachments/assets/c7190286-ffc2-4ba5-ae74-70ffd0a22ae6)
![image](https://github.com/user-attachments/assets/6ac7651d-e92a-4270-bf0e-45dd2f19591c)
![image](https://github.com/user-attachments/assets/1b216467-6088-40a4-951a-64ceba7c16ee)
![image](https://github.com/user-attachments/assets/bdfb5107-06d2-4399-b92e-c384a7183c50)


1. Go to EC2:
   
Login to AWS Console.

Search and open EC2.

2. Launch Instance:
   
Click Launch Instance (top-right).

4. Configure Basic Details:
   
Name: Give a name for your server (example: my-test-server).

Application and OS Image (AMI): Choose an OS (example: Amazon Linux, Ubuntu, Windows, etc.).

Instance Type: Choose size (example: t2.micro is free-tier eligible).

Key Pair (login):

Choose an existing key pair or

Create a new key pair (you need this .pem file to connect later).

4. Configure Network:
   
Select a VPC and Subnet (default is fine if unsure).

Configure Firewall (Security Group):

Allow SSH (port 22) for Linux or RDP (port 3389) for Windows.

You can restrict access to your IP for security.

5. Storage:
   
Default storage is fine (example: 8 GB gp2).

7. Launch:
   
Click Launch Instance.

Wait a minute or two → instance will start running.

ssh -i .pem(file) <user_name>@public_ipaddress

### Connect to EC2

You need Public Ip address, username, .pem file

![image](https://github.com/user-attachments/assets/d03ea1d2-261e-4600-9426-c1ad82e70b1f)


## VPC

![image](https://github.com/user-attachments/assets/8d477246-0f27-441f-9642-a6c82b8ca5c8)

**VPC (Virtual Private Cloud)**

A VPC is like your own private network inside the cloud (e.g., AWS, OCI). You control how resources like servers (EC2 instances) communicate with each other and the internet.

When you create a VPC, you define an IP address range (CIDR block), which determines the size of your VPC. Within that range, you can create subnets to organize and allocate IP addresses for different resources.



**Subnet**

A subnet is a section of your VPC’s IP range.

You split your VPC into subnets to organize and isolate resources.

Subnets can be public (internet-facing) or private (internal only).

**Private IP Address**

Assigned to resources inside a subnet.

Used for internal communication within the VPC.

Not reachable from the internet.

**Public IP Address**

Optional and used for internet access.

Mapped to a private IP on a resource (like a VM or load balancer).

Reachable from the internet.

**Route Table**

Contains rules (routes) that decide where network traffic goes.

Example:

Traffic to 0.0.0.0/0 goes to internet gateway → allows internet access.

Traffic to a specific subnet stays inside the VPC.

**Load Balancer**

Distributes traffic across multiple backend resources (e.g., app servers).

Can be public (internet-facing) or private (internal use).

Helps handle large traffic and increases availability.

The load balancer has access to the private subnet, and the user has access to the load balancer.

**Internet Gateway**

An Internet Gateway (IGW) is a component that allows resources in your VPC to connect to the internet — and also allows the internet to reach them (if they have a public IP and correct route).

Key Points:

It’s attached to a VPC.

It provides a path for internet traffic to and from the VPC.

It works with public subnets where resources (like VMs) need internet access.

🧭 How It Works:

A VM (EC2 instance) in a public subnet has:

A public IP

A route to 0.0.0.0/0 via the Internet Gateway

When the VM sends traffic to the internet:

The route table forwards it to the Internet Gateway.

The public IP is used for the internet to respond.

The Internet Gateway allows bidirectional communication:

Outbound (VM → Internet)

Inbound (Internet → VM, if security rules allow)

## Firewall

A firewall is a network security device or software that monitors and controls incoming and outgoing network traffic based on predefined security rules.

Purpose:
To protect networks and systems from unauthorized access, cyberattacks, or exposure by allowing only trusted traffic.


Securitygroup and NACL

![image](https://github.com/user-attachments/assets/bc47f8db-635c-4cb3-bfc9-2dc3169d18e5)

**SecurityGroup**
A Security Group acts as a virtual firewall for your Amazon EC2 instances to control inbound and outbound traffic. It works at the instance level and it is the last stage

NACL
A Network ACL (NACL) is another layer of security for your VPC that controls traffic at the subnet level.
