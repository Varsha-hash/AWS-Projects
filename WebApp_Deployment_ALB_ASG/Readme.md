## 🌐 Scalable Web Application using ALB & Auto Scaling

### 📌 Project Overview

This project demonstrates how to deploy a **highly available and scalable web application** on AWS using:

- Amazon EC2
- Application Load Balancer (ALB)
- Auto Scaling Group (ASG)

The application automatically scales based on traffic and ensures high availability across multiple Availability Zones.

---

### 🏗️ Architecture

User → ALB → Target Group → Auto Scaling Group → EC2 Instances
---

### 🚀 Deployment Steps

---

### ✅ Step 1: Create Launch Template

1. Navigate to:
AWS Console → EC2 → Launch Templates → Create Launch Template

2. Configure:

- Name: `WebAppTemplate`
- AMI: Amazon Linux 2 / Ubuntu
- Instance Type: t2.micro or t3.medium
- Key Pair: Select existing or create new

---

### 📜 User Data Script

```bash
#!/bin/bash
sudo yum update -y
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
echo "<h1>Welcome to Scalable Web App</h1>" | sudo tee /var/www/html/index.html

Security Group (EC2)
SSH (22) → Your IP
HTTP (80) → ALB Security Group
HTTPS (443) → Optional
```

### ✅ Step 2: Create Auto Scaling Group

---
Navigate to:

EC2 → Auto Scaling Groups → Create Auto Scaling Group

Select:
WebAppTemplate

Configure:
Desired Capacity: 2
Minimum Instances: 1
Maximum Instances: 4

Network
Choose VPC
Select at least 2 subnets (Multi-AZ)

Load Balancer
Choose: Application Load Balancer
Create Target Group:

Target Type: Instance
Protocol: HTTP
Port: 80
Health Check Path: /

---

### Step 3: Create Application Load Balancer

Navigate to:

EC2 → Load Balancers → Create Load Balancer

Configure:
Name: WebAppALB
Scheme: Internet-facing
VPC: Same as ASG
AZs: Minimum 2

Listener
HTTP : 80

Target Group
Select previously created target group

Security Group (ALB)
HTTP (80) → 0.0.0.0/0
HTTPS (443) → Optional

---

### Step 4: Test Application
---
Go to:
EC2 → Load Balancers

Copy ALB DNS
Example:
http://webappalb-xxxx.ap-south-1.elb.amazonaws.com

Open in browser
Output : Welcome to Scalable Web App

---
