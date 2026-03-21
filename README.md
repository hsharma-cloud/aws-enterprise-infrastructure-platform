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

## 🚀 Deployment Steps

```bash
cd terraform
terraform init
terraform validate
terraform plan
terraform apply
