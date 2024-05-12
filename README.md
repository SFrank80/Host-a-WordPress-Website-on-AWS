
---
# Hosting a WordPress Website on AWS

## Project Overview

This project involves deploying a WordPress website on Amazon Web Services, utilizing a robust architecture that ensures high availability, security, and scalability. The website is hosted across multiple EC2 instances within a VPC, leveraging an array of AWS services to optimize performance and manage traffic effectively.

## Architecture Overview

### Components
- **Virtual Private Cloud (VPC)**: Configured with public and private subnets across two Availability Zones to enhance fault tolerance and resource availability.
- **EC2 Instances**: Host the WordPress application within auto-scalable configurations to handle variable load.
- **Application Load Balancer (ALB)**: Distributes incoming traffic across EC2 instances to ensure smooth user experiences and enhance fault tolerance.
- **Auto Scaling Group**: Dynamically scales EC2 instances based on demand to ensure efficient resource utilization.
- **Amazon RDS**: Provides a managed relational database service for WordPress data storage.
- **Amazon EFS**: Implements a scalable file storage solution for managing WordPress content.
- **Amazon Route 53**: Manages DNS records and domain name services for the website.
- **AWS Certificate Manager**: Secures the site with SSL/TLS certificates.
- **Security Groups and IAM Roles**: Ensure secure access and operation of AWS resources.
- **EC2 Instance Connect**: Allows secure SSH access to EC2 instances from the internet.

### Diagram
Insert your architecture diagram here to give a visual overview of the application setup.

## Deployment Strategy

The deployment utilizes several scripts to automate the setup and configuration of the environment, ensuring that the WordPress site is robust and resilient.

### Initial WordPress Setup Script

This script automates the deployment of WordPress on an EC2 instance, including the installation of necessary software components like Apache, PHP, and MySQL.

```bash
#!/bin/bash
# Essential system updates and Apache installation
sudo yum update -y
sudo yum install -y httpd
sudo systemctl start httpd
sudo systemctl enable httpd

# PHP and MySQL installation
sudo amazon-linux-extras install -y php7.4
sudo yum install -y php-mbstring php-xml php-mysqlnd
sudo wget https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm
sudo rpm -ivh mysql57-community-release-el7-11.noarch.rpm
sudo yum install -y mysql-community-server
sudo systemctl start mysqld
sudo systemctl enable mysqld

# WordPress download and configuration
wget https://wordpress.org/latest.tar.gz
tar -xzf latest.tar.gz
sudo cp -r wordpress/* /var/www/html/
cd /var/www/html
sudo cp wp-config-sample.php wp-config.php
# Edit wp-config.php as needed
sudo chown -R apache:apache /var/www/html
sudo systemctl restart httpd
```

### Auto Scaling Launch Configuration

This configuration script ensures that each instance spun up by the Auto Scaling Group is configured correctly and ready to handle web traffic immediately upon launch.

```bash
#!/bin/bash
# Repeat the necessary installation and configuration steps as in the initial setup script
# Ensure all services are set to start on system boot
```

## How to Deploy

1. **Prepare your AWS environment**: Set up the VPC, subnets, and other network resources as outlined in the architecture.
2. **Run the initial setup script**: On your first EC2 instance to deploy WordPress.
3. **Configure Auto Scaling**: Use the launch configuration script for new instances.
4. **Test the deployment**: Ensure that the website is accessible and performs as expected under different loads.

## Monitoring and Maintenance

Leverage AWS CloudWatch for monitoring the performance and health of EC2 instances and the RDS database. Set up alerts to notify of critical issues or high resource usage.

## Security

Ensure that all security groups tightly control traffic flow to and from the instances. Use IAM roles to manage AWS service permissions securely.

---

Replace placeholders with specific commands or URLs as needed. This README is structured to provide a clear, professional overview of your project, demonstrating both your technical skills and your ability to document complex systems effectively.
