---

# Hosting a Static Website on AWS

## Overview
This repository contains scripts and resources to deploy a static HTML web application on AWS. The following components and configurations were utilized.

## Architecture
- **Virtual Private Cloud (VPC):** Configured a VPC with public and private subnets across two availability zones for enhanced reliability and fault tolerance.
- **Internet Gateway:** Deployed an Internet Gateway to facilitate connectivity between VPC instances and the wider Internet.
- **Security Groups:** Established Security Groups as a network firewall mechanism to control traffic to and from instances.
- **Availability Zones:** Leveraged two Availability Zones to enhance system reliability and fault tolerance.
- **Subnets:** 
  - Utilized Public Subnets for infrastructure components like NAT Gateway and Application Load Balancer.
  - Positioned web servers (EC2 instances) within Private Subnets for enhanced security.
- **EC2 Instance Connect:** Implemented EC2 Instance Connect Endpoint for secure connections to assets within both public and private subnets.
- **NAT Gateway:** Enabled instances in private subnets to access the Internet via the NAT Gateway.
- **Web Hosting:** Hosted the website on EC2 Instances.
- **Application Load Balancer (ALB):** Employed an ALB and a target group for evenly distributing web traffic to an Auto Scaling Group of EC2 instances across multiple Availability Zones.
- **Auto Scaling Group:** Utilized an Auto Scaling Group to automatically manage EC2 instances, ensuring website availability, scalability, fault tolerance, and elasticity.
- **Version Control:** Stored web files on GitHub for version control and collaboration.
- **Certificate Manager:** Secured application communications using a Certificate Manager.
- **Simple Notification Service (SNS):** Configured SNS to alert about activities within the Auto Scaling Group.
- **DNS Configuration:** Registered the domain name and set up a DNS record using Route 53.

## Deployment Script
```bash
#!/bin/bash

# Switch to the root user to gain full administrative privileges
sudo su

# Update all installed packages to their latest versions
yum update -y

# Install Apache HTTP Server
yum install -y httpd

# Change the current working directory to the Apache web root
cd /var/www/html

# Install Git
yum install git -y

# Clone the project GitHub repository to the current directory
git clone https://github.com/rnkwilliams/host-a-static-website-on-aws.git

# Copy all files, including hidden ones, from the cloned repository to the Apache web root
cp -R host-a-static-website-on-aws/. /var/www/html/

# Remove the cloned repository directory to clean up unnecessary files
rm -rf host-a-static-website-on-aws

# Enable the Apache HTTP Server to start automatically at system boot
systemctl enable httpd

# Start the Apache HTTP Server to serve web content
systemctl start httpd
```

## Note
Ensure to customize configurations such as domain name, security settings, and scaling policies according to your specific requirements before deployment.

For any issues or inquiries, please refer to the GitHub repository or contact [rnkwilliams](https://github.com/rnkwilliams).

**Disclaimer:** Please ensure the security configurations and best practices are thoroughly reviewed and implemented before deploying any resources in a production environment.

---
