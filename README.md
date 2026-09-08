# aws-infra-project
# AWS Multi-Tier Infrastructure Automation 🚀

[

![Terraform](https://img.shields.io/badge/Terraform-v1.16.1-purple)

](https://terraform.io)
[

![AWS](https://img.shields.io/badge/AWS-Cloud-orange)

](https://aws.amazon.com)
[

![CI/CD](https://img.shields.io/badge/CI%2FCD-GitHub%20Actions-blue)

](https://github.com/features/actions)

## Overview
This project automates the provisioning of a production-grade, multi-tier AWS infrastructure using Terraform. It follows Infrastructure as Code (IaC) best practices with a fully automated CI/CD pipeline via GitHub Actions.

## Architecture



┌─────────────────────────────────────┐
                    │           AWS Cloud (ap-south-1)     │
                    │                                       │
      Internet ──── │ ── Internet Gateway                   │
                    │          │                            │
                    │     Route Table                       │
                    │          │                            │
                    │  ┌───────────────┐  ┌─────────────┐  │
                    │  │ Public Subnet │  │Private Subnet│  │
                    │  │  10.0.1.0/24  │  │ 10.0.2.0/24 │  │
                    │  │               │  │             │  │
                    │  │  EC2 t3.micro │  │  RDS MySQL  │  │
                    │  │  (Web Server) │  │   8.0       │  │
                    │  └───────────────┘  └─────────────┘  │
                    │          │                            │
                    │      S3 Bucket                        │
                    │   (Static Assets)                     │
                    └─────────────────────────────────────┘




                    ## Infrastructure Components

| Resource | Name | Configuration |
|----------|------|--------------|
| VPC | kiran-vpc | CIDR: 10.0.0.0/16 |
| Public Subnet | kiran-public-subnet | CIDR: 10.0.1.0/24, AZ: ap-south-1a |
| Private Subnet | kiran-private-subnet | CIDR: 10.0.2.0/24, AZ: ap-south-1b |
| Internet Gateway | kiran-igw | Attached to VPC |
| Route Table | kiran-public-rt | Routes traffic via IGW |
| Security Group | kiran-sg | Ingress: 22, 80 / Egress: All |
| EC2 Instance | kiran-ec2 | t3.micro, Amazon Linux |
| S3 Bucket | kiran-project-bucket-2024 | Static file storage |
| RDS Instance | kiran-rds | MySQL 8.0, db.t3.micro, 20GB |

## Tech Stack
- **IaC:** Terraform v1.16.1
- **Cloud Provider:** AWS (ap-south-1)
- **CI/CD:** GitHub Actions
- **OS:** Ubuntu Linux
- **Version Control:** Git & GitHub

## CI/CD Pipeline
Every push to `master` branch triggers the pipeline automatically:


## Security Considerations
- AWS credentials stored in **GitHub Secrets** (never hardcoded)
- RDS deployed in **Private Subnet** (no public access)
- Security Groups follow **least privilege principle**
- `.gitignore` excludes sensitive files (`*.pem`, `*.tfstate`)

## Getting Started

### Prerequisites
- AWS Account with IAM credentials
- Terraform v1.0+
- AWS CLI configured

### Deployment
```bash
# Clone the repository
git clone https://github.com/kiranbob2412/aws-infra-project.git
cd aws-infra-project

# Initialize Terraform
terraform init

# Preview changes
terraform plan

# Deploy infrastructure
terraform apply

# Tear down infrastructure
terraform destroy


## Lessons Learned

<h3>🔑 Key Takeaways</h3>

> 💡 **Terraform state management** is critical for team collaboration

> 🔒 **Private subnets** add an essential security layer for databases

> ⚙️ **CI/CD pipelines** catch configuration errors before they reach production

> 👤 **IAM least privilege principle** should always be followed

---

<h2>👨‍💻 Author</h2>

<h3><b>Kiran — Cloud Engineer</b></h3>

[

![GitHub](https://img.shields.io/badge/GitHub-kiranbob2412-black?style=for-the-badge&logo=github)

](https://github.com/kiranbob2412)
