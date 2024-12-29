# AWS CLI Commands

## Links

- [Installation](#installation)
    - [Linux (x86)](#linux-x86)
    - [MacOS Installation](#macos-installation)
    - [Windows Installation](#windows-installation)
- [Initial AWS CLI Configuration](#initial-aws-cli-configuration)
- [EC2 (Elastic Compute Cloud) Commands](#ec2-elastic-compute-cloud-commands)
    - [EC2 Keypair Management](#ec2-keypair-management)
        - [List all keypairs](#list-all-keypairs)
        - [Create a keypair](#create-a-keypair)
        - [Create local keypair (RSA 4096-bit)](#create-local-keypair-rsa-4096-bit)
        - [Import existing keypair](#import-existing-keypair)
        - [Delete keypair](#delete-keypair)
    - [EC2 Image Management](#ec2-image-management)
        - [List private AMIs](#list-private-amis)
        - [Delete AMI](#delete-ami)
    - [EC2 Instance Management](#ec2-instance-management)
        - [List all instances](#list-all-instances)
        - [List running instances](#list-running-instances)
        - [Create new instance](#create-new-instance)
        - [Stop instance](#stop-instance)
        - [List instance status](#list-instance-status)
        - [List specific instance status](#list-specific-instance-status)
        - [List running instances with public IP](#list-running-instances-with-public-ip)
    - [EC2 Security Group Management](#ec2-security-group-management)
        - [List security groups](#list-security-groups)
        - [Create security group](#create-security-group)
        - [Get security group details](#get-security-group-details)
        - [Open port 80](#open-port-80)
        - [Get public IP](#get-public-ip)
        - [Open port 22 for specific IP](#open-port-22-for-specific-ip)
        - [Remove firewall rule](#remove-firewall-rule)
        - [Delete security group](#delete-security-group)
- [IAM (Identity and Access Management) Commands](#iam-identity-and-access-management-commands)
    - [IAM User Management](#iam-user-management)
        - [List all users info](#list-all-users-info)
        - [List usernames](#list-usernames)
        - [Get current user info](#get-current-user-info)
        - [List current user access keys](#list-current-user-access-keys)
        - [Create new user](#create-new-user)
        - [Create multiple users from file](#create-multiple-users-from-file)
        - [Get specific user info](#get-specific-user-info)
        - [Delete user](#delete-user)
        - [Delete all users](#delete-all-users)
    - [IAM Access Key Management](#iam-access-key-management)
        - [List all access keys](#list-all-access-keys)
        - [List user access keys](#list-user-access-keys)
        - [Create access key](#create-access-key)
        - [Get last access time](#get-last-access-time)
        - [Deactivate access key](#deactivate-access-key)
        - [Delete access key](#delete-access-key)
    - [IAM Group and Policy Management](#iam-group-and-policy-management)
        - [List groups](#list-groups)
        - [Create group](#create-group)
        - [Delete group](#delete-group)
        - [List policies](#list-policies)
        - [Get specific policy](#get-specific-policy)
        - [List policy entities](#list-policy-entities)
        - [List group policies](#list-group-policies)
        - [Add policy to group](#add-policy-to-group)
        - [Add user to group](#add-user-to-group)
        - [List group users](#list-group-users)
        - [List user groups](#list-user-groups)
        - [Remove user from group](#remove-user-from-group)
        - [Remove group policy](#remove-group-policy)
- [S3 (Simple Storage Service) Commands](#s3-simple-storage-service-commands)
    - [List buckets](#list-buckets)
    - [List bucket contents](#list-bucket-contents)
    - [Create bucket](#create-bucket)
    - [Remove empty bucket](#remove-empty-bucket)
    - [Copy to bucket](#copy-to-bucket)
    - [Copy from bucket](#copy-from-bucket)
    - [Move object](#move-object)
    - [Sync objects](#sync-objects)
    - [Remove objects](#remove-objects)


## `Installation` :
Instructions for installing AWS CLI on different operating systems.
### Linux (x86)
```
wget "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip"
unzip awscli-exe-linux-x86_64.zip
sudo ./aws/install
```
### MacOS Installation
```
wget "https://awscli.amazonaws.com/AWSCLIV2.pkg"
sudo installer -pkg AWSCLIV2.pkg -target /
```
### Windows Installation
```
Download and run the AWS CLI MSI installer:
msiexec.exe /i https://awscli.amazonaws.com/AWSCLIV2.msi
```
## `Initial AWS CLI Configuration` :
Set up your AWS credentials and default settings:
```
aws configure
AWS Access Key ID [None]: AKIAIOSFODNN7EXAMPLE
AWS Secret Access Key [None]: wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
Default region name [None]: ca-central-1
Default output format [None]: json
```
## `EC2 (Elastic Compute Cloud) Commands` :

### `EC2 Keypair Management` :
Commands for managing EC2 key pairs:
#### List all keypairs
```
aws ec2 describe-key-pairs
```
#### Create a keypair
```
aws ec2 create-key-pair --key-name <keyname> --output text
```
#### Create local keypair (RSA 4096-bit)
```
ssh-keygen -t rsa -b 4096
```
#### Import existing keypair
```
aws ec2 import-key-pair --key-name keyname_test --public-key-material file:///home/user/id_rsa.pub
```
#### Delete keypair
```
aws ec2 delete-key-pair --key-name <keyname>
```
### `EC2 Image Management` :
Commands for managing Amazon Machine Images (AMIs):
#### List private AMIs
```
aws ec2 describe-images --filter "Name=is-public,Values=false" --query 'Images[].[ImageId, Name]' --output text
```
#### Delete AMI
```
aws ec2 deregister-image --image-id ami-00000000
```
### `EC2 Instance Management`:
Commands for managing EC2 instances:
#### List all instances
```
aws ec2 describe-instances
```
#### List running instances
```
aws ec2 describe-instances --filters Name=instance-state-name,Values=running
```
#### Create new instance
```
aws ec2 run-instances --image-id ami-a0b1234 --instance-type t2.micro --security-group-ids sg-00000000 --dry-run
```
#### Stop instance
```
aws ec2 terminate-instances --instance-ids <instance_id>
```
#### List instance status
```
aws ec2 describe-instance-status
```
#### List specific instance status
```
aws ec2 describe-instance-status --instance-ids <instance_id>
```
#### List running instances with public IP
```
aws ec2 describe-instances --filters Name=instance-state-name,Values=running --query 'Reservations[].Instances[].[PublicIpAddress, Tags[?Key==Name].Value | [0] ]' --output text
```
### `EC2 Security Group Management` :
Commands for managing security groups:
#### List security groups
```
aws ec2 describe-security-groups
```
#### Create security group
```
aws ec2 create-security-group --vpc-id vpc-1a2b3c4d --group-name web-access --description "web access"
```
#### Get security group details
```
aws ec2 describe-security-groups --group-id sg-0000000
```
#### Open port 80
```
aws ec2 authorize-security-group-ingress --group-id sg-0000000 --protocol tcp --port 80 --cidr 0.0.0.0/24
```
#### Get public IP
```
my_ipaddress=$(dig +short myip.opendns.com @resolver1.opendns.com); echo $my_ipaddress
```
#### Open port 22 for specific IP
```
aws ec2 authorize-security-group-ingress --group-id sg-0000000 --protocol tcp --port 80 --cidr $my_ipaddress/24
```
#### Remove firewall rule
```
aws ec2 revoke-security-group-ingress --group-id sg-0000000 --protocol tcp --port 80 --cidr 0.0.0.0/24
```
#### Delete security group
```
aws ec2 delete-security-group --group-id sg-00000000
```
## `IAM (Identity and Access Management) Commands` :

### `IAM User Management` :
Commands for managing IAM users:
#### List all users info
```
aws iam list-users
```
#### List usernames
```
aws iam list-users --output text | cut -f 6
```
#### Get current user info
```
aws iam get-user
```
#### List current user access keys
```
aws iam list-access-keys
```
#### Create new user
```
aws iam create-user --user-name UserName
```
#### Create multiple users from file
```
allUsers=$(cat ./user-names.txt)
for userName in $allUsers; do
    aws iam create-user --user-name $userName
done
```
#### Get specific user info
```
aws iam get-user --user-name UserName
```
#### Delete user
```
aws iam delete-user --user-name UserName
```
#### Delete all users
```
allUsers=$(aws iam list-users --output text | cut -f 6)
for userName in $allUsers; do
    aws iam delete-user --user-name $userName
done
```
### `IAM Access Key Management` :
Commands for managing access keys:
#### List all access keys
```
aws iam list-access-keys
```
#### List user access keys
```
aws iam list-access-keys --user-name UserName
```
#### Create access key
```
aws iam create-access-key --user-name UserName --output text | tee UserName.txt
```
#### Get last access time
```
aws iam get-access-key-last-used --access-key-id AKSZZRR7RKZY4EXAMPLE
```
#### Deactivate access key
```
aws iam update-access-key --access-key-id AKIZNAA7RKZY4EXAMPLE --status Inactive --user-name UserName
```
#### Delete access key
```
aws iam delete-access-key --access-key-id AKIZNAA7RKZY4EXAMPLE --user-name UserName
```
### `IAM Group and Policy Management` :
Commands for managing groups and policies:
#### List groups
```
aws iam list-groups
```
#### Create group
```
aws iam create-group --group-name GroupName
```
#### Delete group
```
aws iam delete-group --group-name GroupName
```
#### List policies
```
aws iam list-policies
```
#### Get specific policy
```
aws iam get-policy --policy-arn <arn>
```
#### List policy entities
```
aws iam list-entities-for-policy --policy-arn <arn>
```
#### List group policies
```
aws iam list-attached-group-policies --group-name GroupName
```
#### Add policy to group
```
aws iam attach-group-policy --group-name GroupName --policy-arn arn:aws:iam::aws:policy/AdministratorAccess
```
#### Add user to group
```
aws iam add-user-to-group --group-name GroupName --user-name UserName
```
#### List group users
```
aws iam get-group --group-name GroupName
```
#### List user groups
```
aws iam list-groups-for-user --user-name UserName
```
#### Remove user from group
```
aws iam remove-user-from-group --group-name GroupName --user-name UserName
```
#### Remove group policy
```
aws iam detach-group-policy --group-name GroupName --policy-arn arn:aws:iam::aws:policy/AdministratorAccess
```
## `S3 (Simple Storage Service) Commands` :
Commands for managing S3 buckets and objects:
### List buckets
```
aws s3 ls
```
### List bucket contents
```
aws s3 ls s3://<bucketName>
```
### Create bucket
```
aws s3 mb s3://<bucketName>
```
### Remove empty bucket
```
aws s3 rb s3://<bucketName>
```
### Copy to bucket
```
aws s3 cp <object> s3://<bucketName>
```
### Copy from bucket
```
aws s3 cp s3://<bucketName>/<object> <destination>
```
### Move object
```
aws s3 mv s3://<bucketName>/<object> <destination>
```
### Sync objects
```
aws s3 sync <local> s3://<bucketName>
```
### Remove objects
```
aws s3 rm s3://<bucketName>/<object>
```