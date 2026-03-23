# AWS Enterprise Infrastructure Platform

## 📌 Project Overview

This project demonstrates the design and implementation of a highly available, secure, and scalable AWS infrastructure using Terraform.

It follows AWS best practices for:
- Multi-AZ architecture
- Network segmentation
- Secure internet access
- Infrastructure as Code (IaC)

---

## 🏗️ Architecture Summary

- VPC with CIDR `10.0.0.0/16`
- 2 Availability Zones
- 6 Subnets:
  - Public Subnets (ALB / NAT)
  - Private App Subnets (EC2)
  - Private DB Subnets (RDS)
- Internet Gateway for public access
- NAT Gateway for secure outbound access
- Route Tables for traffic control

---

## ⚙️ Technologies Used

- AWS VPC
- AWS EC2 (upcoming)
- AWS RDS (upcoming)
- AWS NAT Gateway
- AWS Internet Gateway
- Terraform

---

## 📸 Architecture Overview

### 🟦 VPC Overview
![VPC Overview](screenshots/01-vpc-overview.png)

---

### 🟩 Multi-AZ Subnet Architecture
![Subnets](screenshots/02-subnets-multi-az.png)

- Public, Private App, and Private DB subnets
- Distributed across multiple Availability Zones

---

### 🟨 Internet Gateway
![Internet Gateway](screenshots/03-internet-gateway.png)

---

### 🟧 Public Route Table
![Public Route Table](screenshots/04-route-table-public.png)

---

### 🟪 Route Table Associations
![Route Associations](screenshots/05-route-table-associations.png)

---

### 🟥 NAT Gateway
![NAT Gateway](screenshots/06-nat-gateway.png)

---

### 🟫 Private Route Table
![Private Route Table](screenshots/07-private-route-table.png)

---

### 🟦 EC2 Instance (Private Compute)
![EC2 Instance](screenshots/08-ec2-instance.png)

- Deployed in private subnet  
- No public IP  
- Access via SSM  

---

### 🌐 Application Access (ALB)
![ALB Success](screenshots/09-alb-success.png)

- Public access via ALB DNS  
- Confirms end-to-end connectivity  

---

### ⚙️ ALB Configuration
![ALB Details](screenshots/10-alb-details.png)

- Shows DNS endpoint and listener  
- Confirms correct load balancer setup  

---

### 🔁 Auto Scaling Group (High Availability)
![ASG](screenshots/11-asg-instances.png)

- Multiple EC2 instances across subnets  
- Ensures high availability and fault tolerance  

---

# 🗄️ 3. Database Layer

## RDS Instance (Private DB)
![RDS](screenshots/12-rds-instance.png)

---

# 💾 4. Storage Layer

## S3 Bucket (Secure Storage)
![S3](screenshots/13-s3-bucket.png)

## EBS Volume (Block Storage)
![EBS](screenshots/14-ebs-volume.png)

## EFS (Shared File Storage)
![EFS](screenshots/15-efs.png)

---

# 💰 5. Cost Optimization (Domain 4)

## S3 Lifecycle Policy
![S3 Lifecycle](screenshots/16-s3-lifecycle.png)

## Auto Scaling Capacity Optimization
![ASG Capacity](screenshots/17-asg-capacity.png)

## EBS gp3 Optimization
![EBS gp3](screenshots/18-ebs-gp3.png)


---

## 🚀 Deployment Steps

```bash
cd terraform
terraform init
terraform validate
terraform plan
terraform apply
```

---

## 🖥️ Compute Layer

### Overview
The compute layer is designed to securely run application workloads within private subnets while exposing them to users through a controlled entry point.

---

### Key Components

- **Amazon EC2 (Private Subnet)**
  - Deployed without public IP
  - Hosts application (Apache web server)
  - Isolated from direct internet access

- **AWS Systems Manager (SSM)**
  - Secure instance access without SSH
  - Eliminates need for key pairs and open ports
  - Enables centralized management

- **Application Load Balancer (ALB)**
  - Public-facing entry point
  - Distributes traffic to backend EC2 instances
  - Improves availability and scalability

- **Target Group & Health Checks**
  - Routes traffic only to healthy instances
  - Ensures application reliability

- **Security Groups**
  - ALB: allows HTTP (port 80) from internet
  - EC2: allows controlled inbound traffic
  - Enforces least-privilege networking

---

### 🔄 Traffic Flow

```
Internet → ALB → EC2 (Private) → NAT Gateway → Internet
```

---

### Key Features Implemented

- Private compute deployment (no public exposure)
- Secure access using SSM (no SSH)
- Automated provisioning using user data
- Load balancing with health checks
- Multi-tier architecture (public + private separation)
- Controlled outbound internet via NAT Gateway

---

### Benefits

- Enhanced security (no direct access to EC2)
- Scalable architecture (ALB-ready for multiple instances)
- Production-ready design pattern
- Fully automated using Terraform

---

## 🏗️ Architecture Diagram

The following diagram represents the overall architecture of the system.

👉 Open the editable diagram: `diagrams/aws_architecture.drawio`

---

## 🔄 Request Flow

1. User sends request from the internet  
2. Request hits **Application Load Balancer (ALB)**  
3. ALB forwards traffic to **EC2 in private subnet**  
4. EC2 processes request (Apache)  
5. EC2 uses **NAT Gateway** for outbound access  
6. Response returns via ALB  

---

## 🧱 Architecture Diagram (ASCII)

```text
                🌐 Internet
                     │
                     ▼
        ┌──────────────────────────┐
        │   Application Load       │
        │   Balancer (Public)      │
        └──────────┬───────────────┘
                   │
                   ▼
    ┌──────────────────────────────┐
    │     EC2 Instance (Private)   │
    │     Apache Web Server        │
    └──────────┬───────────────────┘
               │
               ▼
    ┌──────────────────────────────┐
    │        NAT Gateway           │
    │   (Outbound Internet Access) │
    └──────────┬───────────────────┘
               │
               ▼
            🌍 Internet


    🔒 VPC: 10.0.0.0/16

    Public Subnets:
    - ALB
    - NAT Gateway

    Private Subnets:
    - EC2 (App Layer)
    - DB Layer (future)
```
