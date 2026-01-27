

---

```markdown
# Terraform Complete Guide – Beginner to Advanced (Production Ready)

Terraform is an **Infrastructure as Code (IaC)** tool by HashiCorp that allows you to provision, manage, and version cloud infrastructure safely and efficiently.

This repository is designed for:
- ✅ Beginners learning Terraform from scratch
- ✅ DevOps engineers building real AWS infrastructure
- ✅ Interview preparation (scenario-based)
- ✅ Production-grade Terraform usage

---

## 📁 Repository Structure

```

## 📁 Repository Structure

```
terraform-complete-guide/
├── README.md
│
├── docs/
│   ├── terraform-basics.md
│   ├── terraform-advanced.md
│   ├── terraform-best-practices.md
│   ├── terraform-security.md
│   └── terraform-interview-questions.md
│
├── labs/
│   ├── lab-01-installation/
│   ├── lab-02-first-ec2/
│   ├── lab-03-variables-outputs/
│   ├── lab-04-vpc/
│   ├── lab-05-modules/
│   ├── lab-06-remote-backend/
│   ├── lab-07-workspaces/
│   ├── lab-08-asg-alb/
│   └── lab-09-production-architecture/
│
├── modules/
│   ├── vpc/
│   ├── ec2/
│   ├── alb/
│   ├── asg/
│   ├── rds/
│   └── security-group/
│
├── environments/
│   ├── dev/
│   ├── qa/
│   └── prod/
│
├── scripts/
│   ├── userdata.sh
│   └── init-backend.sh
│
├── versions.tf
└── .gitignore
```

```

---

## 1️⃣ What is Terraform?

Terraform is an **IaC tool** that allows you to:
- Create infrastructure
- Modify infrastructure
- Destroy infrastructure  
using **declarative configuration files**

Instead of clicking in the AWS Console, you **write code**.

---

## 2️⃣ Why Terraform?

✔ Cloud-agnostic (AWS, Azure, GCP, Kubernetes)  
✔ Declarative & idempotent  
✔ Version-controlled infrastructure  
✔ Reusable modules  
✔ Safe and automated provisioning  

---

## 3️⃣ Terraform Architecture

Terraform consists of:
- Terraform CLI
- Providers
- State file
- Backend

Flow:
```

Terraform CLI → Provider → Cloud API → Infrastructure

````

---

## 4️⃣ Terraform Installation

### Linux
```bash
sudo apt update
sudo apt install terraform -y
````

Verify:

```bash
terraform version
```

---

## 5️⃣ Terraform Workflow

Terraform lifecycle:

```text
terraform init
terraform plan
terraform apply
terraform destroy
```

---

## 6️⃣ Terraform Configuration Language (HCL)

```hcl
resource "aws_instance" "example" {
  ami           = "ami-0abcdef12345"
  instance_type = "t2.micro"
}
```

---

## 7️⃣ Providers

```hcl
provider "aws" {
  region = "us-east-1"
}
```

---

## 8️⃣ Resources

```hcl
resource "aws_s3_bucket" "bucket" {
  bucket = "terraform-demo-bucket"
}
```

---

## 9️⃣ Variables

```hcl
variable "instance_type" {
  default = "t2.micro"
}
```

Usage:

```hcl
instance_type = var.instance_type
```

---

## 🔟 Outputs

```hcl
output "public_ip" {
  value = aws_instance.example.public_ip
}
```

---

## 1️⃣1️⃣ Data Sources

Fetch existing infrastructure:

```hcl
data "aws_ami" "ubuntu" {
  most_recent = true
}
```

---

## 1️⃣2️⃣ State Management

Terraform stores state in:

```
terraform.tfstate
```

⚠️ Never edit state manually
⚠️ Always secure the state file

---

## 1️⃣3️⃣ Backend Configuration (Remote State)

```hcl
terraform {
  backend "s3" {
    bucket         = "terraform-state-prod"
    key            = "prod/terraform.tfstate"
    region         = "us-east-1"
    dynamodb_table = "terraform-lock"
  }
}
```

---

## 1️⃣4️⃣ Terraform CLI Commands

| Command            | Purpose           |
| ------------------ | ----------------- |
| terraform init     | Initialize        |
| terraform plan     | Preview changes   |
| terraform apply    | Apply changes     |
| terraform destroy  | Destroy infra     |
| terraform validate | Validate          |
| terraform fmt      | Format            |
| terraform taint    | Recreate resource |
| terraform state    | State management  |

---

## 1️⃣5️⃣ Provisioners

```hcl
provisioner "remote-exec" {
  inline = ["sudo apt install nginx -y"]
}
```

⚠️ Use only when unavoidable

---

## 1️⃣6️⃣ Modules

Modules allow reusability.

```hcl
module "vpc" {
  source = "./modules/vpc"
}
```

---

## 1️⃣7️⃣ Workspaces

```bash
terraform workspace new dev
terraform workspace select prod
```

---

## 1️⃣8️⃣ Dependencies

Terraform handles dependencies automatically.

Explicit:

```hcl
depends_on = [aws_vpc.main]
```

---

## 1️⃣9️⃣ Lifecycle Rules

```hcl
lifecycle {
  prevent_destroy = true
  create_before_destroy = true
}
```

---

## 2️⃣0️⃣ Functions, Conditions & Loops

```hcl
count = var.create_instance ? 1 : 0
```

```hcl
for_each = var.instances
```

---

## 🧪 Hands-On Labs

### Lab 01 – Installation

✔ Install Terraform
✔ Verify CLI

### Lab 02 – First EC2

✔ Provider
✔ EC2
✔ Security Group

### Lab 03 – Variables & Outputs

✔ Input variables
✔ Output values

### Lab 04 – VPC from Scratch

✔ VPC
✔ Subnets
✔ IGW
✔ Route tables

### Lab 05 – Modules

✔ Create reusable modules
✔ Call modules

### Lab 06 – Remote Backend

✔ S3 state
✔ DynamoDB locking

### Lab 07 – Workspaces

✔ Dev / QA / Prod

### Lab 08 – ALB + ASG

✔ Launch Template
✔ Auto Scaling
✔ Load Balancer

### Lab 09 – Full Production Setup

✔ VPC (Multi-AZ)
✔ ALB
✔ ASG
✔ RDS (Multi-AZ)
✔ NAT Gateway
✔ IAM
✔ Secure networking

---

## ☁️ AWS Production Architecture (Terraform)

```
Internet
   |
Application Load Balancer (Public Subnets)
   |
Auto Scaling Group (Private Subnets)
   |
RDS (Private Subnets, Multi-AZ)
```

### Production Features

✅ High availability
✅ Auto scaling
✅ Zero downtime deployment
✅ Secure IAM
✅ Remote state & locking

---

## 🎯 Terraform Interview Questions

### Beginner

1. What is Terraform?
2. Terraform vs CloudFormation?
3. What is a provider?
4. What is state?

### Intermediate

5. count vs for_each?
6. What if state file is deleted?
7. Local vs remote backend?
8. How Terraform detects drift?

### Advanced

9. Terraform in a team environment?
10. How do you manage secrets?
11. How to prevent deletion?
12. How does Terraform manage dependencies?

---

## 🔥 Scenario-Based Questions

### Scenario 1 – Multiple engineers applying Terraform

✔ Remote backend
✔ DynamoDB locking

### Scenario 2 – Zero downtime deployment

✔ ALB
✔ ASG
✔ create_before_destroy

### Scenario 3 – Same infra for dev/qa/prod

✔ Separate environment folders
✔ OR workspaces

---

## 🔐 Terraform Security Best Practices

✔ IAM least privilege
✔ Encrypt state file
✔ No secrets in code
✔ Use Secrets Manager / Vault
✔ Enable state locking

---

## 🚀 Terraform in CI/CD

Typical pipeline:

1. terraform init
2. terraform validate
3. terraform plan
4. Manual approval
5. terraform apply

Used with:

* Jenkins
* GitHub Actions
* GitLab CI

---

## ✅ Best Practices Summary

✔ Use modules
✔ Use remote backend
✔ Version lock providers
✔ Separate environments
✔ Avoid provisioners
✔ Enable logging

---

## 📚 References

* [https://developer.hashicorp.com/terraform](https://developer.hashicorp.com/terraform)
* [https://registry.terraform.io/](https://registry.terraform.io/)


