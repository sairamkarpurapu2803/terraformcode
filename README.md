# 🏗️ Terraform Infrastructure as Code

<div align="center">

[![Terraform](https://img.shields.io/badge/Terraform-844FBA?style=for-the-badge&logo=terraform&logoColor=white)](https://www.terraform.io/)
[![AWS](https://img.shields.io/badge/AWS-FF9900?style=for-the-badge&logo=amazon-aws&logoColor=white)](https://aws.amazon.com/)
[![HCL](https://img.shields.io/badge/HCL-000000?style=for-the-badge&logo=hashicorp&logoColor=white)](https://www.terraform.io/)

**Automating Cloud Infrastructure Provisioning with Reusable and Scalable IaC Modules**

[Documentation](#overview) • [Quick Start](#quick-start) • [Support](https://github.com/sairamkarpurapu2803/terraformcode/issues)

</div>

---

## 📋 Overview

Enterprise-grade Terraform configurations for AWS infrastructure automation. This repository contains production-ready, modular, and reusable Infrastructure as Code templates for provisioning scalable cloud infrastructure.

### Key Features
- ✅ Modular Terraform structure for reusability
- ✅ Complete VPC with multi-AZ setup
- ✅ EC2 Auto Scaling Groups
- ✅ RDS Database configurations
- ✅ Load Balancers (ALB/NLB)
- ✅ Security Groups & IAM policies
- ✅ S3 buckets with encryption
- ✅ CloudFront CDN integration
- ✅ Route53 DNS management
- ✅ Terraform state management with S3 backend

---

## 🚀 Quick Start

### Prerequisites

```bash
# Install Terraform
brew install terraform  # macOS
# or download from https://www.terraform.io/downloads

# Install AWS CLI
brew install awscli

# Configure AWS credentials
aws configure

# Verify installation
terraform version
aws --version
```

### Initial Setup

1. **Clone the repository**
```bash
git clone https://github.com/sairamkarpurapu2803/terraformcode.git
cd terraformcode
```

2. **Initialize Terraform**
```bash
terraform init
```

3. **Validate configuration**
```bash
terraform validate
```

4. **Format code**
```bash
terraform fmt -recursive
```

---

## 📁 Project Structure

```
terraformcode/
├── environments/
│   ├── dev/
│   ├── staging/
│   └── production/
├── modules/
│   ├── vpc/
│   ├── ec2/
│   ├── rds/
│   ├── alb/
│   └── s3/
├── backend/
│   └── backend.tf
├── variables.tf
├── outputs.tf
└── main.tf
```

---

## 🏢 Modules Overview

### VPC Module
- Multi-AZ deployment
- Public & private subnets
- NAT Gateway
- Internet Gateway
- Route tables & associations

### EC2 Module
- Auto Scaling Groups
- Launch templates
- EBS volume optimization
- CloudWatch monitoring
- IAM instance profiles

### RDS Module
- Multi-AZ deployments
- Automated backups
- Encryption at rest
- Read replicas
- Parameter groups

### ALB Module
- Application Load Balancer
- Target groups
- Health checks
- SSL/TLS certificates
- Access logs

### S3 Module
- Versioning
- Encryption
- Public access blocking
- Lifecycle policies
- Access logging

---

## 📊 Common Workflows

### Plan Infrastructure Changes

```bash
# Plan for specific environment
terraform plan -var-file="environments/production/terraform.tfvars"

# Save plan to file
terraform plan -var-file="environments/production/terraform.tfvars" -out=tfplan
```

### Apply Infrastructure Changes

```bash
# Apply with approval
terraform apply tfplan

# Auto-approve (use with caution!)
terraform apply -var-file="environments/production/terraform.tfvars" -auto-approve
```

### Destroy Infrastructure

```bash
# Plan destruction
terraform plan -destroy -var-file="environments/production/terraform.tfvars"

# Destroy resources
terraform destroy -var-file="environments/production/terraform.tfvars"
```

### State Management

```bash
# List resources in state
terraform state list

# Show specific resource
terraform state show aws_instance.app[0]

# Move resource
terraform state mv aws_instance.app aws_instance.application

# Remove resource (keep in AWS)
terraform state rm aws_instance.app
```

---

## 🔐 Security Best Practices

### Secrets Management

```hcl
# Use AWS Secrets Manager
resource "aws_secretsmanager_secret" "db_password" {
  name = "rds/db/password"
}

# Or use variables with sensitive flag
variable "db_password" {
  type      = string
  sensitive = true
}
```

### IAM Policies

```hcl
# Principle of least privilege
resource "aws_iam_role_policy" "app_policy" {
  name = "app-policy"
  role = aws_iam_role.app_role.id

  policy = jsonencode({
    Version = "2012-10-17"
    Statement = [
      {
        Effect   = "Allow"
        Action   = "s3:GetObject"
        Resource = "${aws_s3_bucket.app_bucket.arn}/*"
      }
    ]
  })
}
```

### Encryption

```hcl
# Enable encryption for all resources
- S3: Enable SSE-KMS
- RDS: Enable encryption at rest
- EBS: Enable encryption
```

---

## 📈 Cost Optimization

### Auto Scaling

```hcl
# Configure scaling policies
resource "aws_autoscaling_policy" "scale_up" {
  name                   = "scale-up"
  autoscaling_group_name = aws_autoscaling_group.app.name
  adjustment_type        = "ChangeInCapacity"
  scaling_adjustment     = 1
  cooldown               = 300
}
```

---

## 🧪 Testing

### Validate Configuration

```bash
terraform validate
terraform fmt -check
```

### Lint with TFLint

```bash
brew install tflint
tflint --init
tflint
```

---

## 📞 Support & Contact

- **Issues**: [GitHub Issues](https://github.com/sairamkarpurapu2803/terraformcode/issues)
- **Email**: sairamkarpurapu2803@gmail.com
- **LinkedIn**: [Sairam Karpurapu](https://www.linkedin.com/in/sairam-karpurapu-22174b2b7)

---

<div align="center">

**Made with ❤️ by Sairam Karpurapu**

*Infrastructure as Code Excellence! 🏗️*

</div>