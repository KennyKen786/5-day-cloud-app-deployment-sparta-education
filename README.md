## Sparta Education UK – 5 Day App Deployment Training

I undertook a 5-day sprint with Sparta Education to deepen my understanding of Cloud Computing and AWS services.

# AWS & DevOps Training Journey Documentation

This repository documents my AWS Cloud & DevOps training journey completed with Sparta Education UK.

The training focused on:

* AWS Cloud Infrastructure
* Linux Server Administration
* Application Deployment
* MongoDB Databases
* Bash Scripting & Automation
* Monitoring & Scaling
* High Availability Architecture
* AWS Networking & Security

---

# Day 1 – AWS & EC2 Fundamentals

## Topics Covered

* Introduction to AWS Cloud Computing
* Launching and configuring EC2 Instances
* Connecting to Linux servers using SSH
* Understanding Ubuntu Linux environments
* Configuring AWS Security Groups
* Opening required ports:

  * Port 22 (SSH)
  * Port 80 (HTTP)
  * Port 3000 (Application)
* Preparing infrastructure for application deployment

## Key Skills Learned

* AWS EC2 provisioning
* Linux terminal basics
* SSH connectivity
* Cloud networking fundamentals
* Security group configuration

---

# Day 2 – Manual Application Deployment

## Application Deployment Workflow

### EC2 Setup

Created an EC2 instance with:

* Port 22 open for SSH
* Port 80 open for HTTP
* Port 3000 open for Node.js application

### Secure File Transfer

Used SCP to transfer application files:

```bash
scp -i ~/.ssh/key.pem app.zip ubuntu@EC2_PUBLIC_IP:~
```

## Manual Deployment Steps

### Update System Packages

```bash
sudo apt update -y
sudo apt upgrade -y
```

### Install Dependencies

```bash
sudo apt install unzip -y
sudo apt install nginx -y
```

### Install Node.js 20.x

```bash
sudo bash -c "curl -fsSL https://deb.nodesource.com/setup_20.x | bash -"
sudo apt install nodejs -y
```

### Install Application Dependencies

```bash
sudo npm install
```

### Start Application

```bash
npm start app.js
```

## Additional Topics Covered

* Nginx reverse proxy configuration
* PM2 process management
* Git & GitHub deployment workflows
* Bash scripting for deployment automation

---

# Day 3 – Automation, MongoDB & Monitoring

## Troubleshooting Node.js Deployment

Resolved module path errors while running MongoDB seed scripts.

### Correct Seed Command

```bash
nodejs app/seeds/seed.js
```

## MongoDB Deployment

### MongoDB Installation

```bash
sudo apt install gnupg curl -y
```

### Configure MongoDB Remote Access

Updated MongoDB configuration:

```bash
bindIp: 0.0.0.0
```

### Start MongoDB Service

```bash
sudo systemctl start mongod
sudo systemctl enable mongod
```

## App Deployment Script

Created an automated deployment script:

```bash
#!/bin/bash

sudo apt update -y
sudo apt upgrade -y
sudo apt install git nginx sed curl -y

git clone https://github.com/LSF970/se-sparta-test-app.git

sudo sed -i '51c\proxy_pass http://127.0.0.1:3000;' /etc/nginx/sites-available/default

sudo systemctl restart nginx
sudo systemctl enable nginx

sudo bash -c "curl -fsSL https://deb.nodesource.com/setup_20.x | bash -"
sudo apt install nodejs -y

cd se-sparta-test-app/app
npm install

sudo npm install pm2 -g
pm2 kill
pm2 start app.js
```

## Database Deployment Script

Created an automated MongoDB deployment script:

```bash
#!/bin/bash

sudo apt update -y
sudo apt upgrade -y

sudo apt install gnupg curl sed -y

curl -fsSL https://www.mongodb.org/static/pgp/server-7.0.asc | \
sudo gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg \
--dearmor

sudo mkdir -p /data/db

sudo sed -i 's/bindIp: 127.0.0.1/bindIp: 0.0.0.0/' /etc/mongod.conf

sudo systemctl start mongod
sudo systemctl enable mongod
```

## AWS Monitoring & Recovery

### Created:

* Amazon Machine Images (AMIs)
* CloudWatch Dashboards
* CloudWatch Alarms
* SNS Notifications

### Monitoring Included:

* CPU Utilisation
* Network Traffic
* Instance Health
* Disk Activity

---

# Day 4 – Scalable Cloud Architecture

## User Data Automation

Used EC2 User Data scripts to automate application startup during instance launch.

## User Data Script

```bash
#!/bin/bash

sleep 15

cd /home/ubuntu/se-sparta-test-app/app

export DB_HOST=mongodb://<DB_IP>:27017/posts

pm2 start app.js
```

## AWS Networking Architecture

### VPC Configuration

* Created a Virtual Private Cloud (VPC)
* Configured Public & Private Subnets
* Worked across multiple Availability Zones
* Configured Route Tables
* Attached Internet Gateway (IGW)

## Security Groups

### Application Security Group

Allowed:

* Port 22 (SSH)
* Port 80 (HTTP)
* Port 3000 (Application)

### Database Security Group

Allowed:

* Port 27017 (MongoDB)
* Restricted access from App Security Group only

## Launch Templates

Created reusable EC2 Launch Templates including:

* Ubuntu AMI
* Instance Type
* Key Pair
* Security Groups
* User Data Scripts

## Application Load Balancer (ALB)

Configured:

* Internet-facing Load Balancer
* Target Groups
* Health Checks
* Traffic Distribution

## Auto Scaling Groups (ASG)

Configured:

* Minimum Capacity
* Desired Capacity
* Maximum Capacity
* CPU-based Scaling Policies
* Multi-AZ High Availability

## Cloud Architecture Concepts Learned

* High Availability
* Scalability
* Fault Tolerance
* Infrastructure Automation
* Self-Healing Infrastructure
* Elastic Cloud Computing

---

# Technologies Used

## AWS Services

* EC2
* VPC
* Security Groups
* AMIs
* Launch Templates
* Auto Scaling Groups
* Application Load Balancer
* CloudWatch
* SNS

## DevOps & Linux Tools

* Ubuntu Linux
* Bash Scripting
* Git & GitHub
* Nginx
* PM2
* SSH
* SCP

## Application Stack

* Node.js
* MongoDB
* Express.js

---

# Key Learning Outcomes

Through this training I gained hands-on experience with:

* Cloud infrastructure deployment
* Linux server administration
* Application deployment workflows
* Infrastructure automation
* Monitoring & alerting
* AWS networking
* Load balancing & scalability
* Database configuration
* Security best practices
* Production-style architecture design

---

# Reflection

This training has provided valuable practical experience in real-world DevOps workflows and cloud engineering practices.

I have learned how modern cloud systems are:

* Deployed
* Automated
* Monitored
* Scaled
* Secured
* Maintained

The journey from manually deploying applications to building scalable and automated AWS infrastructure has been extremely valuable in developing my cloud and DevOps engineering skills.


