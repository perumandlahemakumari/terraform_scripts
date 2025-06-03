# 🌐 Terraform AWS VPC Creation

This project demonstrates how to create a **VPC** using **Terraform** on AWS.

---

## 📦 Prerequisites

- AWS CLI configured (`aws configure`)
- Terraform installed on your system
- IAM user with permissions to manage VPC resources

---

## 📁 Terraform Configuration (main.tf)

### ✅ VPC Creation Script

```hcl
provider "aws" {
  region = "ap-south-1"
}

resource "aws_vpc" "main_vpc" {
  cidr_block           = "10.0.0.0/16"
  enable_dns_support   = true
  enable_dns_hostnames = true

  tags = {
    Name = "MyMainVPC"
    Environment = "Dev"
  }
}

resource "aws_subnet" "main_subnet" {
  vpc_id                  = aws_vpc.main_vpc.id
  cidr_block              = "10.0.1.0/24"
  availability_zone       = "ap-south-1a"
  map_public_ip_on_launch = true

  tags = {
    Name = "MainSubnet"
  }
}

resource "aws_internet_gateway" "gw" {
  vpc_id = aws_vpc.main_vpc.id

  tags = {
    Name = "MainInternetGateway"
  }
}

resource "aws_route_table" "main_route_table" {
  vpc_id = aws_vpc.main_vpc.id

  route {
    cidr_block = "0.0.0.0/0"
    gateway_id = aws_internet_gateway.gw.id
  }

  tags = {
    Name = "MainRouteTable"
  }
}

resource "aws_route_table_association" "a" {
  subnet_id      = aws_subnet.main_subnet.id
  route_table_id = aws_route_table.main_route_table.id
}
```

---

## 🛠️ Terraform Commands

```bash
terraform init                   # Initialize Terraform
terraform plan                   # Preview the plan
terraform apply --auto-approve  # Apply the infrastructure changes
terraform destroy --auto-approve # Destroy the infrastructure
```

---

## 📌 Notes

- Update the CIDR blocks if needed.
- Make sure to destroy VPC components in the reverse order to avoid dependency issues.

---

## 🧹 Clean Up

```bash
terraform destroy --auto-approve
```

---

## 🧾 License

This project is for demonstration and learning purposes.
