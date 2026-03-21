# aws-enterprise-infrastructure-platform
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

- Enables public internet access
- Attached to enterprise VPC

---

### 🟧 Public Route Table
![Public Route Table](screenshots/04-route-table-public.png)

- Routes internet traffic (0.0.0.0/0 → IGW)
- Associated with public subnets

---

### 🟪 Route Table Associations
![Route Associations](screenshots/05-route-table-associations.png)

- Public subnets linked to public route table

---

### 🟥 NAT Gateway
![NAT Gateway](screenshots/06-nat-gateway.png)

- Enables outbound internet access for private subnets
- Deployed in public subnet with Elastic IP

---

### 🟫 Private Route Table
![Private Route Table](screenshots/07-private-route-table.png)

- Routes private traffic through NAT Gateway
- Associated with application and database subnets
