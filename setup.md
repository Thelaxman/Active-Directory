# Setup Instructions for Active Directory Management on AWS

## Introduction

This document provides step-by-step instructions for setting up the AWS environment and configuring a Windows Server instance with Active Directory Domain Services (AD DS).

## AWS Environment Setup

### Step 1: Create a Virtual Private Cloud (VPC)

If you don't already have a VPC, create one by following these steps:

1. Go to the **VPC Dashboard** in the AWS Management Console.
2. Click **Create VPC** and follow the wizard to set up:
   - **CIDR block**: `10.0.0.0/16` (or your preferred range).
   - **Subnets**: Create both public and private subnets for your EC2 instances.
   - **Route tables**: Ensure that your public subnet has a route to the internet (via an Internet Gateway).

### Step 2: Create Security Groups

1. In the **VPC Dashboard**, navigate to **Security Groups**.
2. Create a new security group for your EC2 instance with the following inbound rules:
   - **RDP (3389)**: Allow from your IP (for secure access).
   - **Custom TCP**: Allow traffic on port 389 for AD DS and other necessary ports (like DNS, LDAP, etc.).

## Launching the Windows Server EC2 Instance

### Step 1: Launch EC2 Instance

1. Go to the **EC2 Dashboard** and click **Launch Instance**.
2. Choose a **Windows Server AMI** (e.g., Windows Server 2019 or newer).
3. Choose an instance type (e.g., `t2.medium` or higher for better performance).
4. Configure instance details:
   - Select your VPC and subnet.
   - Ensure **Auto-assign Public IP** is enabled for external access.
5. Set up the security group to use the one created earlier.
6. Review and launch the instance.

### Step 2: Assign IAM Role (if needed)

1. In the **IAM Dashboard**, create or assign an IAM role that grants necessary EC2 permissions, such as access to Directory Service if you're syncing with AWS IAM later.
2. Attach the role to the EC2 instance during the launch process.

## Connecting to the Windows Server Instance

### Step 1: Get RDP Credentials

1. After the instance is running, select it from the **EC2 Dashboard**.
2. Click **Connect**, then choose **RDP Client**.
3. Download the **RDP file** and click **Get Password**.
4. Upload your key pair to decrypt the administrator password.
5. Save the password for later use.

### Step 2: Connect via RDP

1. Use an RDP client (such as Microsoft Remote Desktop) to connect to your Windows instance using the public IP address and the decrypted password.

## Configuring Windows Server

### Step 1: Update Windows Server

1. Once connected, open **Windows Update** and install any pending updates.
2. Restart the server if necessary.

### Step 2: Configure Static IP (optional but recommended)

1. Open **Control Panel** > **Network and Sharing Center** > **Change adapter settings**.
2. Right-click your network adapter, select **Properties**, then select **Internet Protocol Version 4 (TCP/IPv4)**.
3. Set a static IP (e.g., `10.0.0.10`) for consistency, and ensure the subnet mask and default gateway match your VPC settings.

## Installing Active Directory Domain Services (AD DS)

### Step 1: Add Active Directory Domain Services Role

1. Open **Server Manager** and click **Add roles and features**.
2. Select **Active Directory Domain Services** under the **Roles** section.
3. Complete the wizard and install the AD DS role.

### Step 2: Promote the Server to a Domain Controller

1. After the role is installed, in **Server Manager**, click the yellow triangle in the top right and select **Promote this server to a domain controller**.
2. Choose **Add a new forest** and set the **Root domain name** (e.g., `example.com`).
3. Set a **Directory Services Restore Mode (DSRM)** password.
4. Complete the wizard and allow the server to restart.

### Step 3: Verify AD DS Installation

1. After the server reboots, log in using the **domain administrator** credentials you set up.
2. Open **Active Directory Users and Computers** to verify the domain controller is working correctly.

## Verifying the Setup

### Step 1: Test Domain Controller Functionality

1. Use the **Active Directory Users and Computers** console to check if the domain is active.
2. Verify that you can create and manage users in the domain.

### Step 2: Test Network Connectivity

1. Ensure that DNS resolution is working by pinging the domain controller using the domain name (e.g., `ping example.com`).
2. Verify that the EC2 instance is properly communicating within the VPC and can access other resources as needed.

---
