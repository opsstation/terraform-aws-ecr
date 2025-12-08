#  🏗️ Terraform-AWS-ECR

[![OpsStation](https://img.shields.io/badge/Made%20by-OpsStation-blue?style=flat-square&logo=terraform)](https://www.opsstation.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Terraform](https://img.shields.io/badge/Terraform-1.13%2B-purple.svg?logo=terraform)](#)
[![CI](https://github.com/OpsStation/terraform-aws-ec2/actions/workflows/ci.yml/badge.svg)](https://github.com/OpsStation/terraform-aws-ec2/actions/workflows/ci.yml)

> 🌩️ **A production-grade, reusable AWS Ec2 module by [OpsStation](https://www.opsstation.com)**
> Designed for reliability, performance, and security — following AWS networking best practices.
---


## 🏢 About OpsStation

**OpsStation** delivers **Cloud & DevOps excellence** for modern teams:
- 🚀 **Infrastructure Automation** with Terraform, Ansible & Kubernetes
- 💰 **Cost Optimization** via scaling & right-sizing
- 🛡️ **Security & Compliance** baked into CI/CD pipelines
- ⚙️ **Fully Managed Operations** across AWS, Azure, and GCP

> 💡 Need enterprise-grade DevOps automation?
> 👉 Visit [**www.opsstation.com**](https://www.opsstation.com) or email **hello@opsstation.com**

---
## 🌟 Features

- ✅ Creates and manages **AWS Elastic Container Registry (ECR) repositories** using Terraform
- ✅ Supports both **Private** and **Public** ECR repositories
- ✅ Automatically configures required **IAM Roles & IAM Policies** for secure image push/pull operations
- ✅ Enables **image scanning**, **KMS encryption**, and **repository policies** for enhanced security
- ✅ Supports **image tag immutability**, **scan-on-push**, and **lifecycle policies** for automated image retention
- ✅ Allows **cross-account** and **cross-region replication** for multi-environment and disaster recovery setups
- ✅ Integrates seamlessly with **ECS**, **EKS**, **Lambda (container image functions)**, and CI/CD pipelines
- ✅ Provides repository-level settings such as **tag mutability**, **encryption configuration**, and **scan options**
- ✅ Supports resource tagging and naming through the **Labels module**
- ✅ Follows AWS best practices for **container security**, **artifact management**, and **repository governance**
- ✅ Fully compatible with other **OpsStation Terraform modules**
---

# Example : private_ecr
```hcl
module "private_ecr" {
  source             = "git::https://github.com/opsstation/terraform-aws-ecr.git?ref=v1.0.0"
  enable_private_ecr = true
  name               = local.name
  environment        = local.environment
  scan_on_push       = true
  max_image_count    = 7
}
```

# Example : public_ecr
```hcl
module "public_ecr" {
  source                   = "git::https://github.com/opsstation/terraform-aws-ecr.git?ref=v1.0.0"
  enable_public_ecr        = true
  name                     = local.name
  environment              = local.environment
  max_untagged_image_count = 1
  max_image_count          = 7
  public_repository_catalog_data = {
    description       = "Docker container for some things"
    operating_systems = ["Linux"]
    architectures     = ["x86"]
  }
}
```

### 🔐 Outputs (AWS ECR Module)

| Name                      | Description                                                                 |
|---------------------------|-----------------------------------------------------------------------------|
| `repository_arn`          | The **ARN of the ECR repository**.                                          |
| `repository_name`         | The **name of the ECR repository**.                                         |
| `repository_url`          | The **URL of the repository** used for Docker image push/pull operations.   |
| `registry_id`             | The **AWS account ID** that owns the registry.                              |
| `repository_policy`       | The **IAM policy** applied to the ECR repository.                           |
| `lifecycle_policy`        | The **lifecycle policy** attached to the repository (if enabled).           |
| `image_tag_mutability`    | The **tag mutability setting** (`MUTABLE` or `IMMUTABLE`).                  |
| `scan_on_push`            | Indicates whether **image vulnerability scanning** is enabled.              |
| `encryption_type`         | The **encryption setting** of the repository (`AES256` or `KMS`).           |
| `kms_key_arn`             | The **KMS key ARN** used for image encryption (if KMS enabled).             |
| `replication_configuration`| The **cross-region or cross-account replication config** (if enabled).     |
| `tags`                    | A mapping of **tags** assigned to the ECR repository.                       |
---
### ☁️ Tag Normalization Rules (AWS)

| Cloud | Case      | Allowed Characters | Example                            |
|--------|-----------|------------------|------------------------------------|
| **AWS** | TitleCase | Any              | `Name`, `Environment`, `CostCenter` |
---
### 💙 Maintained by [OpsStation](https://www.opsstation.com)
> OpsStation — Simplifying Cloud, Securing Scale.