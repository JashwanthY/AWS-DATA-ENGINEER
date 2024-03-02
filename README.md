# How to Configure AWS SFTP Server with AWS S3

This guide provides step-by-step instructions on configuring an AWS SFTP server with AWS S3.

## Prerequisites
- AWS account with necessary permissions

## Steps

### 1. Create S3 Bucket
- Log in to the AWS Management Console.
- Navigate to the S3 service.
- Create a new bucket with a unique name and desired configuration settings.

### 2. AWS Transfer Family - Create SFTP Server
- Log in to the AWS Management Console.
- Navigate to the AWS Transfer Family service.
- Select "Create Server".
- Choose the protocols you want to enable, select "SFTP".
- Choose an identity provider - "Service Managed".
- Configure endpoint settings as "Publicly accessible".
- Choose a domain - "Amazon S3".
- Click on Next, Review and create.
- Review the configuration and click "Create".

### 3. Create User in SFTP Server
- Navigate to the AWS Transfer Family service.
- Select the created server.
- Create a username, select an IAM role for S3 access, and specify an AWS S3 bucket.
- Create an IAM role:
  - Click on "Create role".
  - Scroll down, search and select "Transfer" and click next.
  - Choose an IAM policy. [Example Policy](https://github.com/JashwanthY/AWS-DATA-ENGINEER/blob/main/IAM%20policy%20SFTP%20-%20S3)
  - Copy the policy, click on JSON, paste the policy, create a policy name, and click on create policy.
  - Select the created policy, click next, choose a role name, and create a role.
- Click on "Add User" in AWS Transfer Family - SFTP Server.
- Create a username, choose the roles created earlier, select an S3 bucket, choose a root directory, and click on "restricted".
- Click on "Add".

### 4. Create an SSH Key
- Use the following command to create a key:
  ```bash
  ssh-keygen -m PEM -f key_name
- Choose a passphrase.
- Open the key_name.pub file, copy the text, and paste it into SSH public key settings in the SFTP server.

### 5. Connect your SFTP Server
- Connect to your SFTP server with the following command:
  ```bash
  sftp -i <your_private_key> <username>@<sftp_dns_host>
- Enter the passphrase for the key created earlier.
- Try listing your AWS S3 Bucket with ls.

### 6. Upload and Download a File
- To upload a file, use the put command:
  ```bash
  sftp> put ae.xml
- To download a file, use the get command:
  ```bash
  sftp> get ae.xml
