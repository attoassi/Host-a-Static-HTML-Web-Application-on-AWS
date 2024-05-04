## Hosting a Static Website on AWS

### Overview

This project demonstrates the process of hosting a static HTML web application on AWS (Amazon Web Services) infrastructure. By following the steps outlined in this guide, you can set up a scalable, reliable, and secure environment for deploying your static website.

### Architecture Diagram

The architecture for hosting the static website on AWS involves several components and configurations:

![AWS Architecture Diagram](architecture_diagram.png)

### Step-by-Step Guide

Follow these steps to deploy your static website on AWS:

1. **Configuring Virtual Private Cloud (VPC)**:
   - Set up a VPC with public and private subnets across different availability zones (AZs) for fault tolerance and scalability.

2. **Deploying Internet Gateway (IGW)**:
   - Create an IGW to facilitate connectivity between VPC instances and the wider Internet.

3. **Establishing Security Groups**:
   - Configure security groups to act as a network firewall mechanism, controlling inbound and outbound traffic to EC2 instances.

4. **Utilizing Multiple Availability Zones**:
   - Leverage multiple AZs to enhance system reliability and fault tolerance.

5. **Utilizing Public Subnets**:
   - Use public subnets for infrastructure components like the NAT Gateway and Application Load Balancer (ALB) for external communication.

6. **Implementing EC2 Instance Connect Endpoint**:
   - Set up EC2 Instance Connect Endpoint for secure connections to assets within both public and private subnets.

7. **Positioning Web Servers in Private Subnets**:
   - Place web servers (EC2 instances) within private subnets for enhanced security.

8. **Enabling Internet Access via NAT Gateway**:
   - Enable instances in private subnets to access the Internet through the NAT Gateway.

9. **Hosting Website on EC2 Instances**:
   - Deploy the static website files on EC2 instances.

10. **Employing Application Load Balancer (ALB)**:
    - Set up an ALB and a target group to evenly distribute web traffic to an Auto Scaling Group of EC2 instances across multiple AZs.

11. **Utilizing Auto Scaling Group**:
    - Configure Auto Scaling Group to automatically manage EC2 instances, ensuring website availability, scalability, fault tolerance, and elasticity.

12. **Version Control and Collaboration**:
    - Store web files on GitHub for version control and collaboration purposes.

13. **Securing Application Communications**:
    - Secure application communications using AWS Certificate Manager.

14. **Configuring Simple Notification Service (SNS)**:
    - Set up SNS to alert about activities within the Auto Scaling Group.

15. **Domain Name Registration and DNS Setup**:
    - Register the domain name and configure DNS records using Route 53.

### Deployment Script

Below is a sample deployment script to automate the setup process:

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
git clone https://github.com/attoassi/host-a-static-website-on-aws.git

# Copy all files, including hidden ones, from the cloned repository to the Apache web root
cp -R host-a-static-website-on-aws/. /var/www/html/

# Remove the cloned repository directory to clean up unnecessary files
rm -rf host-a-static-website-on-aws

# Enable the Apache HTTP Server to start automatically at system boot
systemctl enable httpd

# Start the Apache HTTP Server to serve web content
systemctl start httpd
```

### Conclusion

By following this guide and utilizing the provided deployment script, you can successfully host your static website on AWS with scalability, reliability, and security in mind. This setup ensures optimal performance and availability for your web application.
