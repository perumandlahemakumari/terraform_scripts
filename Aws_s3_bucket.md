# ☁️ Terraform AWS S3 Bucket Creation

This project demonstrates how to create an **AWS S3 Bucket** using **Terraform**.

---

## 📦 Prerequisites

- Amazon Linux 2 EC2 instance or local machine with Terraform
- AWS CLI configured (`aws configure`)
- IAM user with S3 full access

---

## ⚙️ Steps to Install Terraform on Amazon Linux

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

### ✅ S3 Bucket Resource

```hcl
resource "aws_s3_bucket" "hema_bucket" {
  bucket = var.bucket_name
  acl    = "private"

  tags = {
    Name        = var.bucket_tag
    Environment = "Dev"
  }
}
```

### ✅ Variables

```hcl
variable "bucket_name" {
  type    = string
  default = "hema-unique-s3-bucket-123456"
}

variable "bucket_tag" {
  type    = string
  default = "HemaBucket"
}
```

---

## 🛠️ Terraform Commands

```bash
terraform init                    # Initialize Terraform
terraform plan                    # Review the execution plan
terraform apply --auto-approve   # Create the S3 bucket
terraform destroy --auto-approve # Delete the S3 bucket
```

---

## 📌 Notes

- The bucket name must be globally unique across all AWS users.
- Avoid hardcoding sensitive information; use `aws configure` or environment variables.

---

## 🧹 Clean Up

```bash
terraform destroy --auto-approve
```

---

## 🧾 License

This project is for demo and educational purposes.
