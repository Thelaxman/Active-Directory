# AWS IAM Integration with Active Directory

## Overview

This guide details how to synchronize Active Directory (AD) users with AWS Identity and Access Management (IAM). By integrating AD with AWS IAM, administrators can manage user access and permissions across AWS resources using AD credentials.

## Prerequisites

- Active Directory set up on an AWS EC2 Windows Server instance
- AWS IAM permissions to manage identity federation
- AWS CLI installed and configured
- AWS Directory Service enabled
- AD Connector or AWS Managed Microsoft AD configured

## Step 1: Set Up AWS Directory Service

1. **Sign in to the AWS Management Console**

   - Navigate to **AWS Directory Service**.
   - Choose **Set up a directory**.
   - Select **AWS Managed Microsoft AD** or **AD Connector** (depending on your needs).
   - Follow the setup wizard to complete the directory setup.

2. **Verify Directory Status**
   - Once the directory is set up, ensure its status is **Active** before proceeding.

## Step 2: Configure IAM Identity Center (SSO) for AD Authentication

1. **Enable AWS IAM Identity Center**

   - Go to **AWS IAM Identity Center** in the AWS Console.
   - Enable **IAM Identity Center** and select **Microsoft AD** as the identity source.

2. **Connect IAM Identity Center to AD**

   - Select the directory you set up in Step 1.
   - Assign users and groups from AD to IAM Identity Center.

3. **Assign AWS Account Access to AD Users**
   - Navigate to **AWS IAM Identity Center** → **Users and Groups**.
   - Select an AD user or group and assign AWS accounts with specific roles.
   - Define permission sets as required.

## Step 3: Sync AD Users with AWS IAM

1. **Retrieve AD Users from Windows Server**

   - Log in to your AD domain controller and run the following PowerShell command:
     ```powershell
     Get-ADUser -Filter * | Select-Object SamAccountName, UserPrincipalName
     ```
   - This will display a list of all AD users.

2. **Manually Create IAM Users (Optional)**

   - In the AWS Console, navigate to **IAM** → **Users**.
   - Add IAM users that match AD users if needed.

3. **Automate IAM User Creation via AWS CLI**
   - Export AD users to a CSV file:
     ```powershell
     Get-ADUser -Filter * | Select-Object SamAccountName, UserPrincipalName | Export-Csv -Path C:\users.csv -NoTypeInformation
     ```
   - Use AWS CLI to create IAM users:
     ```bash
     while IFS=, read -r username email; do
       aws iam create-user --user-name "$username" --tags Key=email,Value="$email"
     done < users.csv
     ```

## Step 4: Assign IAM Roles Based on AD Groups

1. **Create IAM Roles for AD Groups**

   - Navigate to **IAM** → **Roles**.
   - Select **Create Role**.
   - Choose **AWS Directory Service** as the trusted entity.
   - Attach policies based on permissions required.

2. **Map AD Groups to IAM Roles**
   - Use AWS CLI to create mappings:
     ```bash
     aws iam add-role-to-instance-profile --instance-profile-name ADAdmins --role-name AdminRole
     ```
   - Assign users to groups in AD that correspond to IAM roles.

## Step 5: Test and Verify Integration

1. **Test AWS Access with an AD User**

   - Use an AD user to log into AWS IAM Identity Center.
   - Confirm that the assigned permissions and roles are correctly applied.

2. **Check IAM and AD Synchronization Logs**
   - Monitor **AWS CloudTrail** and **Windows Event Viewer** for authentication logs.
