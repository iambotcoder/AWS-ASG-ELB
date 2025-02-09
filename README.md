# 🚀 Scale and Load Balance Your Architecture

---

## 📖 Overview

This project is a simple demonstration of creating and running a scalable and highly available architecture using **AWS EC2 Auto Scaling** and **Elastic Load Balancing (ELB)**. It covers setting up an **Application Load Balancer (ALB)** to distribute traffic across multiple EC2 instances and configuring an **Auto Scaling Group (ASG)** to manage the instances based on demand.

---

## 📑 Table of Contents
- [🔑 Prerequisites](#-prerequisites)
- [🗺️ Architecture](#-architecture)
- [🛠️ Setup & Installation](#-setup--installation)
  - [1⃣ Create an AMI](#1%EF%B8%8F-create-an-ami)
  - [2⃣ Create an Application Load Balancer (ALB)](#2%EF%B8%8F-create-an-application-load-balancer-alb)
  - [3⃣ Configure a Launch Template](#3%EF%B8%8F-configure-a-launch-template)
  - [4⃣ Create an Auto Scaling Group](#4%EF%B8%8F-create-an-auto-scaling-group)
- [📝 Tasks](#-tasks)
  - [Task 1: Create AMI](#task-1-create-ami)
  - [Task 2: Configure ALB](#task-2-configure-alb)
  - [Task 3: Set Up Auto Scaling](#task-3-set-up-auto-scaling)
  - [Task 4: Verify Setup](#task-4-verify-setup)
- [🗑️ Cleaning Up Resources](#%EF%B8%8F-cleaning-up-resources)
- [✅ Conclusion](#-conclusion)
- [📚 Reference](#-reference)

---

## 🔑 Prerequisites
Before you start, ensure you have the following:
- A **Lab VPC** configured
- An **EC2 instance** with a running **web server**
- A **Web Server Security Group (SG)** allowing HTTP (port 80) traffic to instances

---

## 🗺️ Architecture

The application consists of the following components:
- **Application Load Balancer (ALB)**: Distributes incoming traffic across EC2 instances.
- **Auto Scaling Group (ASG)**: Automatically scales the number of instances based on demand.
- **EC2 Instances**: Serve the web application and are launched using a predefined AMI.

### Workflow:
1. Create an **AMI** from an existing EC2 instance.
2. Set up an **Application Load Balancer (ALB)**.
3. Configure a **Launch Template** to define instance settings.
4. Create an **Auto Scaling Group (ASG)** linked to the launch template.
5. Verify the setup by testing the ALB endpoint.

---

## 🛠️ Setup & Installation

### 1⃣ Create an AMI
- In the AWS Management Console, navigate to **EC2** > **Instances**.
- Select an existing instance and click **Create Image**.
- Provide a name and description, then click **Create Image**.

### 2⃣ Create an Application Load Balancer (ALB)
- Navigate to **EC2** > **Load Balancers** > **Create Load Balancer**.
- Select **Application Load Balancer** and provide necessary details.
- Configure **target groups** and **listeners**.

### 3⃣ Configure a Launch Template
- Go to **EC2** > **Launch Templates**.
- Click **Create Launch Template**, provide the AMI ID, instance type, security group, and user data (if needed).

### 4⃣ Create an Auto Scaling Group
- Navigate to **EC2** > **Auto Scaling Groups**.
- Click **Create Auto Scaling Group** and link it to the **Launch Template**.
- Define **desired, minimum, and maximum instance counts**.
- Attach the **ALB Target Group**.

---

## 📝 Tasks

### Task 1: Create AMI
- Create an AMI from an existing EC2 instance.

### Task 2: Configure ALB
- Set up an **Application Load Balancer** with a **target group**.

### Task 3: Set Up Auto Scaling
- Configure a **Launch Template** and **Auto Scaling Group**.

### Task 4: Verify Setup
- Test the ALB endpoint to ensure requests are routed correctly.

---

## 🗑️ Cleaning Up Resources
To clean up all resources, delete them in the following sequence:
1. **Auto Scaling Group**
2. **Launch Template**
3. **Application Load Balancer**
4. **Target Group**
5. **EC2 Instances and AMI**

---

## ✅ Conclusion
This project demonstrated how to set up **AWS EC2 Auto Scaling** and **Application Load Balancing** to create a highly available and scalable architecture. By configuring an **ALB** and an **Auto Scaling Group**, we ensured efficient load distribution and automated scaling based on demand.

---

## 📚 Reference
This project was inspired by **AWS Restart Canvas Lab: 174-[JAWS]-Lab - Scale and Load Balance your Architecture**.
