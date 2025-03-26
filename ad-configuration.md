# Active Directory Configuration on AWS

## Overview

This guide outlines the steps to set up Active Directory (AD) on an AWS EC2 Windows Server instance. The configuration includes installing Active Directory Domain Services (AD DS), promoting the server as a domain controller, and verifying the setup.

## Prerequisites

- An AWS EC2 instance running Windows Server (2019 or later recommended)
- Administrator access to the Windows Server instance
- A properly configured VPC with DNS settings to support AD DS
- RDP access to the instance

## Step 1: Install Active Directory Domain Services (AD DS)

1. **Connect to the EC2 instance**

   - Use RDP to connect to your Windows Server instance.

2. **Open Server Manager**

   - Click on the **Start** menu and open **Server Manager**.

3. **Add Roles and Features**
   - In **Server Manager**, select **Manage** → **Add Roles and Features**.
   - Click **Next** until you reach **Server Roles**.
   - Check **Active Directory Domain Services** and click **Next**.
   - Click **Install** and wait for the installation to complete.

## Step 2: Promote the Server to a Domain Controller

1. **Open Server Manager**

   - Click on the **flag icon** (notification area) and select **Promote this server to a domain controller**.

2. **Configure Deployment**

   - Choose **Add a new forest** and enter your domain name (e.g., `example.local`).
   - Click **Next**.

3. **Set Domain Controller Options**

   - Leave default selections for **Domain Name System (DNS)** and **Global Catalog (GC)**.
   - Set a **Directory Services Restore Mode (DSRM) password**.
   - Click **Next**.

4. **Verify NetBIOS Name**

   - Ensure the NetBIOS name is correct (usually the first part of the domain name) and click **Next**.

5. **Configure Paths and Review Settings**
   - Keep default paths for the database, log files, and SYSVOL folder.
   - Review the configuration summary and click **Install**.
   - The server will restart after installation.

## Step 3: Verify Active Directory Installation

1. **Check Active Directory Users and Computers (ADUC)**

   - After reboot, log in and open **Active Directory Users and Computers** (`dsa.msc`).
   - Verify that the domain and default containers (e.g., Users, Computers) are created.

2. **Test Domain Connectivity**
   - Open a **Command Prompt** and run:
     ```powershell
     nslookup example.local
     ```
   - Ensure it resolves to the domain controller’s IP.
