# dare-aws-cli

A set of helper scripts to make your life a little easier in AWS. 

Current Features:
    - Securely storing credentials in your Mac OS X keychain
    - AWS credentials switching and looping
    - AWS role assume and looping

## Installation & Setup

Time to setup your environment. The dare-aws-cli-setup script adds etc/dare-aws-cli.rc to your .profile or .bash_profile

1. Clone or download this repo and runt the setup script.

    ``` 
    # git clone https://github.com/daringway/dare-aws-cli.git
    # dare-aws-cli/bin/dare-aws-cli-setup 
    ```
1. Start a new bash session

## Overview

All commands start with 'aws-' for easy tab completion.  Most commands have the -? and -h option.

WARNING: Commands that are not listed below are still in development and subject to change.

## aws-cred-add

Security store you AWS credentials.  Currently only support on Mac OS X to store in your keychain.

## aws-cred 

AWS Credential Switching. 

aws-cred is built-in function that allows easy switching between AWS Credentials.

Credentials can exist in either ~/./aws/credentials or in Mac OS X keychain (see aws-cred-add)

If you do not specify a credential a list of options will be presented. 

## aws-cred-loop

This commands allows you to loop over a set AWS credentials. The search order is
1. --cred comma_list_of_creds
1. environment variable $AWSLOOPCREDS in comma seperate list
1. output from aws-cred-list

```
# export AWSLOOPACCOUNTS="cred1 cred2 cred5"
# aws-cred-loop ec2 describe-instances
```

## aws-role 

AWS Assume Role.  aws-role is a built-in function that allows easy AWS assume role. Same functionality as aws-cred but for roles.

Roles are configured in the ~/.aws/roles in the following format.  exteranl_id is optional.

```
[role arbitrary-name-identifier]
account = 123456789012  
role = role/IAM-ROLE-NAME
external_id = 123456789
```

## aws-role-loop

This commands allows you to loop over a set AWS roles. The search order is
1. --cred comma_list_of_roles
1. environment variable $AWSLOOPROLES in comma seperate list
1. output from aws-role-list

## aws-ec2-ssh (alias assh)

Assist with login into an EC2 instance and use specified keyname if found.  aws-ec2-ssh will search all meta 
data associated with the each EC2.  If one match is found it will automatically ssh to the instance.
If multiple instances are found you will be prompted to select.

keyname files use the following search option in ~/.aws/keys
1. <keyname>+<cred-name>.pem
2. <keyname>.pem

```
# aws-cred my-dev-cred
# assh adminhost
```