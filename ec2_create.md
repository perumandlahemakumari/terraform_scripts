# 🚀 Terraform AWS EC2 Instance Deployment on Amazon Linux

This project demonstrates how to set up and deploy an EC2 instance using **Terraform** on an **Amazon Linux 2** server.

---

## 📦 Prerequisites

- Amazon Linux 2 EC2 instance
- AWS CLI configured (`aws configure`)
- IAM user with EC2 full access

---

## ⚙️ Steps to Install Terraform

```bash
sudo su -
sudo yum-config-manager --add-repo https://rpm.releases.hashicorp.com/AmazonLinux/hashicorp.repo
sudo yum install -y terraform
terraform -version
```

---

## 📁 Terraform Configuration (main.tf)

### ✅ Provider Block

```hcl
provider "aws" {
  region = "ap-south-1"
}
```

### ✅ Resource Block

```hcl
resource "aws_instance" "one" {
  ami           = var.ami_id
  instance_type = var.itype
  count         = var.icount

  tags = {
    Name = var.iname
  }
}
```

### ✅ Variables

```hcl
variable "iname" {
  type    = string
  default = "Hema-Instance"
}

variable "ami_id" {
  type    = string
  default = "ami-0f340b1771dc25029"
}

variable "itype" {
  type    = string
  default = "t2.micro"
}

variable "icount" {
  type    = number
  default = 1
}
```
---

## OR

# 📁 simple main.tf

```hcl
provider "aws" {
  region     = "ap-south-1"        
  access_key = "access_keys"   
  secret_key = "secret_keys" 
}

resource "aws_instance" "one" {
  ami                    = "ami-0f340b1771dc25029"
  instance_type          = "t2.micro"
  availability_zone      = "ap-south-1a"
  key_name               = "hema"
  count                  = 1

  tags = {
    Name        = "Terraform_Instance"
    Environment = "Dev"
    Project     = "swiggy"
  }
}
```

---

## 🛠️ Terraform Commands

```bash
terraform init            # Initialize Terraform
terraform plan            # Review execution plan
terraform apply --auto-approve   # Apply the configuration
terraform destroy --auto-approve # Destroy the infrastructure
```

---

## 📌 Notes

- Change the AMI ID if needed for your region.
- Ensure the key pair (`hema`) exists in the AWS region.
- Do **not** hardcode `access_key` and `secret_key` in production. Use `aws configure` or environment variables.

---

## 🧹 Clean Up

```bash
terraform destroy --auto-approve
```

---

## 🧾 License

This project is for demo and educational purposes.
