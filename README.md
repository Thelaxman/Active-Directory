# Active Directory Management on AWS

## Project Overview

This project demonstrates how to set up and manage Active Directory (AD) on an AWS EC2 Windows Server instance, synchronize the AD users with AWS IAM, and manage user permissions. The goal of this project is to integrate traditional AD infrastructure with AWS identity management to provide centralized user and permissions management.

## Project Objectives

- Set up an EC2 Windows Server instance with Active Directory Domain Services (AD DS).
- Create and manage users within the Windows Active Directory.
- Sync the AD users with AWS IAM to reflect them as IAM users or roles.
- Manage permissions and roles for AD users directly from AWS.
- Test and verify the integration to ensure proper functionality.

## Project Structure

This project contains multiple markdown files that document each step and configuration in detail. Below is the structure of the project documentation:

```bash
project-root/
├── README.md            # Project overview, objectives, and main steps
├── setup.md             # Initial setup instructions
├── ad-configuration.md  # Details on setting up AD on Windows Server
├── aws-iam.md           # Syncing AD users with AWS IAM
├── permissions.md       # Managing roles and permissions
├── troubleshooting.md   # Common issues and solutions
└── resources.md         # Useful links and references


```

## Prerequisites

- AWS Account with appropriate permissions.
- Basic understanding of AWS services (EC2, IAM, VPC).
- Familiarity with Windows Server and Active Directory.
- AWS CLI configured on your local machine.

## Technologies Used

- AWS EC2 (Windows Server)
- Active Directory Domain Services (AD DS)
- AWS IAM
- AWS Directory Service
- AWS CLI

## Getting Started

1. Clone the repository to your local machine:
   ```bash
   git clone https://github.com/your-username/your-repo.git
   ```
2. Follow the setup instructions in setup.md to initialize the environment.

3. Proceed with the Active Directory configuration as documented in ad-configuration.md.

4. Sync users to IAM as outlined in aws-iam.md.

5. Assign roles and permissions as per the steps in permissions.md.

## Contributing

Feel free to open issues or submit pull requests if you would like to contribute to this project.
