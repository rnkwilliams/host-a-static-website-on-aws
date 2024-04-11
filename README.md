![Alt text](/Host_a_Static_Website_on_AWS.png)

---
# Hosting a Static Website on AWS

## Overview

This project focuses on deploying a static HTML web application on Amazon Web Services (AWS) infrastructure. Utilizing various AWS services and configurations, we ensure the security, reliability, and scalability of the hosted web application.

## Infrastructure Setup

1. **Virtual Private Cloud (VPC):**
   - Configured a VPC with both public and private subnets across two availability zones for enhanced redundancy and fault tolerance.

2. **Internet Gateway (IGW):**
   - Deployed an Internet Gateway to facilitate connectivity between VPC instances and the wider Internet.

3. **Security Groups:**
   - Established Security Groups as a network firewall mechanism to control traffic to EC2 instances.

4. **Availability Zones (AZs):**
   - Leveraged two Availability Zones to enhance system reliability and fault tolerance.

5. **Subnet Configuration:**
   - Utilized Public Subnets for infrastructure components like the NAT Gateway and Application Load Balancer.
   - Positioned web servers (EC2 instances) within Private Subnets for enhanced security.

6. **EC2 Instance Connect Endpoint:**
   - Implemented EC2 Instance Connect Endpoint for secure connections to assets within both public and private subnets.

## Deployment Process

1. **Deployment Script:**
   - Provided a deployment script for automating the setup process.
   - The script installs necessary packages, clones the project repository from GitHub, and configures Apache HTTP Server to serve web content.

2. **GitHub Integration:**
   - Stored web files on GitHub for version control and collaboration.

## Scalability and Reliability

1. **Auto Scaling Group (ASG):**
   - Employed an Auto Scaling Group to automatically manage EC2 instances.
   - Ensured website availability, scalability, fault tolerance, and elasticity.

2. **Application Load Balancer (ALB):**
   - Utilized an Application Load Balancer and a target group for evenly distributing web traffic across multiple Availability Zones.

## Security Measures

1. **Certificate Manager:**
   - Secured application communications using a Certificate Manager.

2. **Simple Notification Service (SNS):**
   - Configured Simple Notification Service (SNS) to alert about activities within the Auto Scaling Group.

## Domain Configuration

1. **Route 53:**
   - Registered the domain name and set up a DNS record using Route 53.

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

## Conclusion

Ensure to customize configurations such as domain name, security settings, and scaling policies according to your specific requirements before deployment.

For any issues or inquiries, please refer to the GitHub repository or contact rnkwilliams.

**Disclaimer:** Please ensure the security configurations and best practices are thoroughly reviewed and implemented before deploying any resources in a production environment.

--- 
