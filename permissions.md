# Managing Permissions and Roles in AWS IAM for Active Directory Users

## Overview

This guide covers how to assign and manage permissions for Active Directory (AD) users in AWS Identity and Access Management (IAM). By mapping AD users and groups to IAM roles, administrators can enforce security policies and control access to AWS resources effectively.

## Prerequisites

- Active Directory integrated with AWS IAM
- AWS Directory Service configured
- IAM roles created for AD user groups
- AWS CLI installed and configured

## Step 1: Define IAM Roles and Policies

1. **Identify Access Requirements**

   - Determine what AWS services and resources each AD group needs access to.
   - Plan permission levels (e.g., Read-only, Admin, Developer).

2. **Create IAM Policies**
   - Navigate to **IAM** → **Policies** in the AWS Console.
   - Click **Create policy** and define JSON-based permissions.
   - Example JSON for read-only access to S3:
     ```json
     {
       "Version": "2012-10-17",
       "Statement": [
         {
           "Effect": "Allow",
           "Action": "s3:ListBucket",
           "Resource": "*"
         }
       ]
     }
     ```
   - Attach policies to IAM roles.

## Step 2: Assign IAM Roles to AD Groups

1. **Create IAM Roles**

   - Navigate to **IAM** → **Roles** → **Create role**.
   - Select **AWS Directory Service** as the trusted entity.
   - Attach the appropriate policies.

2. **Map AD Groups to IAM Roles**
   - Use AWS CLI to map AD groups to IAM roles:
     ```bash
     aws iam add-role-to-instance-profile --instance-profile-name Developers --role-name DeveloperRole
     ```
   - Assign users in Active Directory to groups that correspond to IAM roles.

## Step 3: Verify Permissions

1. **Test User Access**

   - Log in as an AD user and access AWS resources.
   - Verify that the assigned permissions are correctly enforced.

2. **Monitor IAM Permissions**
   - Use **AWS CloudTrail** and **IAM Access Analyzer** to review user activity.

## Step 4: Modify and Revoke Permissions

1. **Modify IAM Role Policies**

   - Navigate to **IAM** → **Roles** → Select role → Edit permissions.

2. **Remove Users from AD Groups**
   - Update group memberships in Active Directory to revoke AWS access.
