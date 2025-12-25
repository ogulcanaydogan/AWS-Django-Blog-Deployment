# BlogDjango - Scalable Django Deployment on AWS

Production-oriented deployment of a Django-based blog application on AWS, designed to demonstrate high availability, secure networking, and scalable infrastructure using managed AWS services.

## Overview
This project showcases how a Django web application can be deployed in a production-like AWS environment using an Application Load Balancer, Auto Scaling EC2 instances, and an RDS MySQL database inside a custom VPC. Static and media assets are stored on Amazon S3, distributed securely via CloudFront, and exposed to users through Route 53 with failover support.

The infrastructure and deployment flow reflect the responsibilities of a DevOps engineer operating a real-world web platform.

---

## Architecture Summary
- Custom VPC with public and private subnets
- Application Load Balancer in front of EC2 Auto Scaling Group
- EC2 instances running Django application
- Amazon RDS (MySQL 8.0.28) for relational data
- Amazon S3 for static assets and user-uploaded media
- Amazon CloudFront for global content delivery
- Amazon Route 53 with DNS and failover configuration
- DynamoDB table for tracking S3 object metadata
- AWS Lambda triggered by S3 events

---

## Problem Context
A Django blog application developed by a frontend/backend team must be deployed into a secure and highly available production environment. The DevOps responsibility includes:

- Designing isolated network infrastructure
- Deploying and scaling the application
- Securing traffic and data
- Integrating managed AWS services for reliability and performance

The application must be accessible securely from anywhere via a web browser.

---

## Infrastructure Components

### Networking
- Custom VPC
- Public and private subnets
- Internet Gateway
- Route tables and endpoints

### Security
- Dedicated security groups for:
  - Application Load Balancer
  - EC2 instances
  - RDS database
  - NAT instance
- Least-privilege traffic flow (ALB -> EC2 -> RDS)

### Compute and Scaling
- EC2 Launch Template
- Auto Scaling Group
- User data scripts for automated instance bootstrap
- NAT instance in public subnet

### Data Layer
- Amazon RDS
  - Engine: MySQL
  - Version: 8.0.28
  - Subnet group in private subnets

### Storage and Content Delivery
- Two S3 buckets:
  - Media uploads
  - Static website hosting
- CloudFront distribution in front of ALB and S3
- Route 53 DNS with failover routing

### Event-Driven Components
- DynamoDB table for S3 object metadata
- AWS Lambda function
- S3 event notifications triggering Lambda

---

## Application Deployment Flow
1. Clone application source code from the internal repository
2. Prepare a dedicated GitHub repository for deployment
3. Configure Django settings with:
   - RDS endpoint
   - S3 bucket names
4. Create EC2 launch template with user data scripts
5. Deploy Application Load Balancer and target groups
6. Create Auto Scaling Group using the launch template
7. Configure HTTPS certificates for secure access
8. Place CloudFront distribution in front of the ALB
9. Configure Route 53 with DNS records and failover rules
10. Set up S3 events, Lambda, and DynamoDB integration

---

## Server Specifications
- **Operating System:** Ubuntu Server 20.04

---

## Project Structure
```text
BlogDjango
├── README.md                # Project definition and deployment overview
├── src/                     # Django application source code
├── requirements.txt         # Python dependencies
├── lambda_function.py       # Lambda function triggered by S3 events
└── developer_notes.txt      # Deployment and configuration notes
