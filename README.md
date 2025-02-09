# 🚀 Scale and Load Balance Your Architecture

---

## 📖 Overview

This project is a simple demonstration of creating and running a scalable and load-balanced architecture using AWS services like EC2, Auto Scaling, and Elastic Load Balancer (ELB). The goal is to distribute traffic across multiple instances for high availability and reliability.

---

## 📑 Table of Contents

- [🔑 Prerequisites](#-prerequisites)
- [🗺️ Architecture](#-architecture)
- [Task 1: Create a Launch Template](#task-1-create-a-launch-template)
- [Task 2: Configure an Auto Scaling Group](#task-2-configure-an-auto-scaling-group)
- [Task 3: Create and Configure an Elastic Load Balancer](#task-3-create-and-configure-an-elastic-load-balancer)
- [Task 4: Testing and Monitoring](#task-4-testing-and-monitoring)
- [🗑️ Cleaning Up Resources](#-cleaning-up-resources)
- [✅ Conclusion](#-conclusion)
- [Reference](#reference)

---

## 🔑 Prerequisites
Before you start, ensure you have the following:

- **Lab VPC** configured for hosting the instances
- **EC2 Instance** named as Web Server instance
- **Web Server Security Group (SG)** allowing HTTP traffic to instances

---

## 🗺️ Architecture
![AutoScaling Architecture](https://github.com/user-attachments/assets/eabe30d8-5bf7-43af-a8d6-efd4e074c28e)

The application consists of the following components:
- **Ec2 Instance** To host Application.
- **Auto Scaling Group** to dynamically adjust instance count
- **Elastic Load Balancer (ELB)** to distribute traffic

### 🔄 Workflow:
1. Create a Launch Template with the necessary configuration.
2. Set up an Auto Scaling Group with scaling policies.
3. Configure an Application Load Balancer and target groups.
4. Test and monitor the setup for scaling and load balancing.

---

## 📝 Task 1: Creating an AMI for Auto Scaling
1. Navigate to the **Amazon EC2 Management Console**.
2. Select **Instances** from the left panel.
3. Locate and select **Web Server 1** (running state).
4. Click **Actions > Image and templates > Create image**.
5. Configure the following:
   - **Image Name**: `Bot-AMI-Webserver`
   - **Image Description**: `Bot-AMI-Webserver`
6. Click **Create image** and note down the **AMI ID**.

---

## 📝 Task 2: Creating a Load Balancer
1. Navigate to **Load Balancers** under the **EC2 Management Console**.
2. Click **Create load balancer** > Select **Application Load Balancer**.
3. Configure:
   - **Name**: `Bot-ELB`
   - **VPC**: `Lab VPC`
   - **Availability Zones**: Select **Public Subnet 1 & 2**.
4. Remove the default **Security Group** and select **Web Security Group**.
5. Click **Create target group**, configure:
   - **Target Type**: `Instances`
   - **Target Group Name**: `Bot-target-group`
6. Click **Next** > **Create target group**.
7. Return to the Load Balancer page, click **Refresh** on **Forward to**, select `Bot-target-group`.
8. Click **Create load balancer** and note the **DNS name**.

---

## 📝 Task 3: Creating a Launch Template
1. Navigate to **Launch Templates** under **EC2**.
2. Click **Create launch template**.
3. Configure:
   - **Launch Template Name**: `Bot-Ec2-Instance-template`
   - **Description**: `A web server for the load test app`
   - **Auto Scaling Guidance**: Enabled
   - **AMI**: Select `Bot-AMI-Webserver`
   - **Instance Type**: `t3.micro`
   - **Security Group**: `Web Security Group`
4. Click **Create launch template**.

---

## 📝 Task 4: Creating an Auto Scaling Group
1. Select `Bot-Ec2-Instance-template`, click **Actions > Create Auto Scaling Group**.
2. Configure:
   - **Name**: `Lab Auto Scaling Group`
   - **VPC**: `Lab VPC`
   - **Subnets**: `Private Subnet 1 & 2`
3. Attach to an existing **Load Balancer**:
   - Select **Bot-target-group | HTTP**
   - **Health Check Type**: `ELB`
4. Configure Group Size:
   - **Desired Capacity**: `2`
   - **Minimum Capacity**: `2`
   - **Maximum Capacity**: `4`
5. Enable **Target Tracking Scaling Policy**:
   - **Metric Type**: `Average CPU Utilization`
   - **Target Value**: `50%`
6. Skip optional sections and click **Create Auto Scaling Group**.

---

## 📝 Task 5: Verifying Load Balancer Functionality
1. Navigate to **EC2 Instances**.
2. Ensure **two instances** named `Lab Instance` are running.
3. Navigate to **Target Groups** and select `Bot-target-group`.
4. Confirm both instances are **healthy**.
5. Copy the **Load Balancer DNS name**, paste it into a browser, and verify the Load Test application is accessible.

---


## 🗑️ Cleaning Up Resources

To clean up all resources, delete them in the following order:

1. **Auto Scaling Group**
   - Go to **EC2 Dashboard** → **Auto Scaling Groups**.
   - Select the Auto Scaling Group and click **Delete**.

2. **Load Balancer**
   - Go to **EC2 Dashboard** → **Load Balancers**.
   - Select the Load Balancer and click **Delete**.

3. **Target Group**
   - Go to **EC2 Dashboard** → **Target Groups**.
   - Select the Target Group and click **Delete**.

4. **Launch Template**
   - Go to **EC2 Dashboard** → **Launch Templates**.
   - Select the Launch Template and click **Delete**.

5. **EC2 Instances** (if any remain)
   - Go to **EC2 Dashboard** → **Instances**.
   - Select instances and click **Terminate**.

6. **Security Groups (Optional)**
   - Go to **EC2 Dashboard** → **Security Groups**.
   - Select unused security groups and delete them.

7. **VPC (Optional, if created specifically for this project)**
   - Go to **VPC Dashboard** → **VPCs**.
   - Select the VPC and delete it.

---

## ✅ Conclusion

In this project, we successfully created a scalable and load-balanced architecture using AWS Auto Scaling and Elastic Load Balancer. This setup improves availability and ensures efficient traffic distribution.

---

## Reference

This project was inspired by AWS Restart Canvas Lab: **174-[JAWS]-Lab - Scale and Load Balance Your Architecture**.
