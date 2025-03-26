# Troubleshooting Active Directory and AWS IAM Integration

## Overview

This document provides solutions to common issues encountered when integrating Active Directory (AD) with AWS IAM. It covers troubleshooting steps for directory setup, user synchronization, permission issues, and common connectivity problems.

## Common Issues and Solutions

### Issue 1: Directory Service Status is Not Active

**Problem:** The AWS Managed Microsoft AD or AD Connector status is not **Active**.

**Solution:**

1. Ensure that the VPC and security group settings allow traffic on the required ports (e.g., 389, 636, 3268, 3269 for AD).
2. Verify that the directory is properly configured and no other errors appear in the **AWS Directory Service** console.
3. If the directory is stuck in a pending or failed state, try rebooting the directory or contact AWS support for assistance.

### Issue 2: AD Users Not Syncing to AWS IAM

**Problem:** AD users are not syncing to IAM as expected.

**Solution:**

1. Ensure that the **AWS Directory Service** is properly set up and integrated with IAM Identity Center.
2. Check if IAM Identity Center is connected to the correct AD directory.
3. Use the **AWS CLI** to verify that the AD users are available for synchronization:
   ```bash
   aws iam list-users
   ```
4. If users are not appearing, check the AWS CloudTrail logs for any errors related to IAM synchronization.

   ```

   ```

### Issue 3: Insufficient Permissions for AD Users in AWS

**Problem:** AD users cannot access AWS resources despite being assigned roles.

**Solution:**

1. Verify that the appropriate IAM roles and policies are attached to the AD users via IAM Identity Center.
2. Check the IAM policies assigned to AD users and ensure they allow the required permissions for AWS resources.
3. Ensure that the user is logging in using the correct identity provider (e.g., AWS IAM Identity Center).
4. Review AWS CloudTrail logs to identify any permission-denied errors or access issues.

### Issue 4: AD Group Mapping to IAM Role Fails

**Problem:** AD group mappings to IAM roles fail to sync.

**Solution:**

1. Confirm that the AD group is properly mapped to an IAM role.
2. Use the AWS CLI to check the mapping:

```bash
        aws iam get-role --role-name <role-name>
```

3. Ensure that the correct IAM role policies are attached and that there are no conflicts in the permissions.
4. If the AD group mapping is not being reflected, manually remove and re-add the group mapping.

### Issue 5: AD User Login Fails in IAM Identity Center

**Problem:** AD user login fails when attempting to use AWS IAM Identity Center.

**Solution:**

1. Verify that the user has been assigned the necessary permissions and AWS account access through IAM Identity Center.
2. Check if the user has been correctly synchronized with IAM Identity Center.
3. Ensure that multi-factor authentication (MFA) is set up correctly, if required.
4. Review the Windows Event Viewer and AWS CloudTrail logs for any authentication errors.

## General Troubleshooting Tips

- Always ensure that your directory and IAM service are correctly connected and have the right permissions.
- Regularly check AWS CloudTrail for logs to identify any issues related to user authentication or permission denials.
- Use the AWS CLI to verify user and role mappings.
- In case of persistent issues, reach out to AWS support for more detailed assistance.
