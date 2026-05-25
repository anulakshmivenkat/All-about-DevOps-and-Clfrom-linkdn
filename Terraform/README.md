# Terraform for DevOps Engineers

# Introduction

Terraform is an Infrastructure as Code (IaC) tool developed by HashiCorp.

Terraform automates:
- cloud infrastructure provisioning
- networking
- Kubernetes clusters
- storage
- IAM
- security groups
- load balancers

Terraform supports:
- AWS
- Azure
- GCP
- Kubernetes
- VMware
- GitHub
- Docker

---

# What is Infrastructure as Code?

Infrastructure as Code means:
- managing infrastructure using code
- version controlling infrastructure
- automating provisioning

Benefits:
- consistency
- automation
- scalability
- repeatability
- faster deployments

---

# Why Terraform?

Before Terraform:
- manual infrastructure creation
- inconsistent environments
- human errors
- slow provisioning

Terraform solves:
- infrastructure automation
- environment consistency
- reusable infrastructure
- scalable deployments

---

# Terraform Architecture

Terraform consists of:

| Component | Purpose |
|---|---|
| Provider | connects Terraform to platforms |
| Resource | infrastructure object |
| State File | tracks infrastructure |
| Module | reusable Terraform code |

---

# Install Terraform

# Update Packages

Purpose:
- updates package metadata

Command:

```bash
sudo apt update
```

---

# Install Required Packages

Purpose:
- installs dependencies

Command:

```bash
sudo apt install gnupg software-properties-common curl -y
```

---

# Add HashiCorp GPG Key

Purpose:
- verifies Terraform packages

Command:

```bash
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
```

---

# Add Terraform Repository

Purpose:
- adds HashiCorp package source

Command:

```bash
sudo apt-add-repository \
"https://apt.releases.hashicorp.com $(lsb_release -cs) main"
```

---

# Install Terraform

Purpose:
- installs Terraform CLI

Command:

```bash
sudo apt install terraform -y
```

---

# Verify Terraform Installation

Purpose:
- checks Terraform version

Command:

```bash
terraform version
```

---

# Terraform Workflow

1. Write Terraform code
2. Initialize Terraform
3. Validate code
4. Generate execution plan
5. Apply infrastructure
6. Destroy infrastructure when not needed

---

# Create Terraform Project

Purpose:
- creates project directory

Command:

```bash
mkdir terraform-project
```

Move inside:

```bash
cd terraform-project
```

---

# Create Terraform File

Purpose:
- stores infrastructure code

Command:

```bash
vim main.tf
```

---

# Basic Terraform Example

Example:

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "web" {
  ami           = "ami-xxxxxxxx"
  instance_type = "t2.micro"
}
```

---

# Terraform Initialization

Purpose:
- downloads providers
- initializes project

Command:

```bash
terraform init
```

---

# Validate Terraform Code

Purpose:
- checks syntax errors

Command:

```bash
terraform validate
```

---

# Format Terraform Code

Purpose:
- formats Terraform files

Command:

```bash
terraform fmt
```

---

# Generate Execution Plan

Purpose:
- previews infrastructure changes

Command:

```bash
terraform plan
```

---

# Apply Infrastructure

Purpose:
- creates infrastructure resources

Command:

```bash
terraform apply
```

Auto approve:

```bash
terraform apply -auto-approve
```

---

# View Terraform State

Purpose:
- displays tracked resources

Command:

```bash
terraform state list
```

---

# Destroy Infrastructure

Purpose:
- removes provisioned resources

Command:

```bash
terraform destroy
```

---

# Variables

Variables make Terraform reusable.

---

# Create Variables File

Purpose:
- stores reusable inputs

Command:

```bash
vim variables.tf
```

Example:

```hcl
variable "instance_type" {
  default = "t2.micro"
}
```

---

# Outputs

Outputs display resource information.

---

# Create Output

Purpose:
- shows useful values

Example:

```hcl
output "instance_ip" {
  value = aws_instance.web.public_ip
}
```

---

# Terraform State File

Terraform stores infrastructure state in:

```bash
terraform.tfstate
```

Important:
- never manually edit state file

---

# Remote Backend

Remote backend stores state remotely.

Benefits:
- collaboration
- state locking
- security

---

# AWS S3 Backend Example

```hcl
terraform {
  backend "s3" {
    bucket = "terraform-state-bucket"
    key    = "prod/terraform.tfstate"
    region = "us-east-1"
  }
}
```

---

# State Locking

State locking prevents simultaneous changes.

Usually implemented using:
- DynamoDB
- Terraform Cloud

---

# Terraform Modules

Modules create reusable infrastructure.

Benefits:
- standardization
- scalability
- reusability

---

# Module Example

```hcl
module "vpc" {
  source = "./modules/vpc"
}
```

---

# Terraform Workspaces

Workspaces manage environments.

Examples:
- dev
- test
- prod

---

# Create Workspace

Purpose:
- creates separate environment

Command:

```bash
terraform workspace new dev
```

---

# List Workspaces

Purpose:
- displays environments

Command:

```bash
terraform workspace list
```

---

# Switch Workspace

Purpose:
- changes active environment

Command:

```bash
terraform workspace select prod
```

---

# Terraform Lifecycle Rules

Lifecycle controls resource behavior.

Example:

```hcl
lifecycle {
  prevent_destroy = true
}
```

---

# Terraform with AWS

Terraform commonly provisions:
- EC2
- VPC
- S3
- IAM
- EKS
- Route53

---

# Terraform with Kubernetes

Terraform can manage:
- namespaces
- deployments
- services
- ingress

---

# Drift Detection

Terraform detects infrastructure drift.

Purpose:
- identifies manual changes

Command:

```bash
terraform plan
```

---

# Terraform Security Best Practices

- use remote backend
- enable state locking
- never commit secrets
- use IAM roles
- restrict permissions
- encrypt state files

---

# Terraform Troubleshooting

# Validate Syntax

Purpose:
- detects syntax errors

Command:

```bash
terraform validate
```

---

# View Logs

Purpose:
- debug Terraform issues

Command:

```bash
TF_LOG=DEBUG terraform apply
```

---

# Refresh State

Purpose:
- syncs Terraform state

Command:

```bash
terraform refresh
```

---

# Force Unlock State

Purpose:
- removes stuck lock

Command:

```bash
terraform force-unlock LOCK_ID
```

---

# Show Current State

Purpose:
- displays infrastructure details

Command:

```bash
terraform show
```

---

# 50 Most Used Terraform Commands

| Command | Purpose |
|---|---|
| terraform init | initialize project |
| terraform validate | validate configuration |
| terraform fmt | format files |
| terraform plan | preview changes |
| terraform apply | create infrastructure |
| terraform destroy | remove infrastructure |
| terraform show | display state |
| terraform output | display outputs |
| terraform state list | list resources |
| terraform state show | resource details |
| terraform refresh | refresh state |
| terraform taint | mark resource recreate |
| terraform untaint | remove taint |
| terraform import | import resource |
| terraform graph | dependency graph |
| terraform workspace new | create workspace |
| terraform workspace list | list workspaces |
| terraform workspace select | switch workspace |
| terraform providers | provider details |
| terraform login | Terraform Cloud login |
| terraform logout | logout |
| terraform version | version info |
| terraform console | interactive console |
| terraform force-unlock | unlock state |
| terraform get | download modules |
| terraform init -upgrade | upgrade providers |
| terraform apply -auto-approve | auto approve |
| terraform destroy -auto-approve | auto destroy |
| terraform plan -out | save plan |
| terraform apply PLANFILE | apply saved plan |
| terraform state rm | remove resource |
| terraform state mv | move resource |
| terraform state pull | download state |
| terraform state push | upload state |
| terraform providers lock | provider lock |
| terraform workspace delete | delete workspace |
| terraform fmt -recursive | recursive formatting |
| terraform validate -json | JSON validation |
| terraform plan -destroy | destroy preview |
| terraform apply -replace | replace resource |
| terraform output -json | JSON outputs |
| terraform show -json | JSON state |
| terraform graph | dependency visualization |
| terraform login | authenticate |
| terraform metadata | metadata |
| terraform providers mirror | mirror providers |
| terraform state list | list tracked resources |
| terraform state show | inspect state |
| terraform init -reconfigure | reconfigure backend |
| terraform apply -parallelism | parallel resource creation |

---

# Real World Production Scenarios

# Scenario 1 — State File Corruption

Symptoms:
- Terraform fails unexpectedly

Investigation:
- inspect remote backend
- check backup state

Fix:
- restore backup state

---

# Scenario 2 — Resource Drift

Symptoms:
- infrastructure manually modified

Investigation:

```bash
terraform plan
```

Fix:
- reapply Terraform

---

# Scenario 3 — State Lock Issue

Symptoms:
- another operation holds lock

Fix:

```bash
terraform force-unlock LOCK_ID
```

---

# Scenario 4 — Provider Authentication Failure

Symptoms:
- AWS authentication errors

Investigation:
- IAM permissions
- AWS credentials
- environment variables

---

# Scenario 5 — Resource Already Exists

Symptoms:
- Terraform cannot create resource

Fix:

```bash
terraform import
```

---

# Production Troubleshooting Workflow

# Step 1 — Validate Configuration

```bash
terraform validate
```

---

# Step 2 — Format Code

```bash
terraform fmt
```

---

# Step 3 — Generate Plan

```bash
terraform plan
```

---

# Step 4 — Enable Debug Logs

```bash
TF_LOG=DEBUG terraform apply
```

---

# Step 5 — Verify State

```bash
terraform state list
```

---

# Step 6 — Verify Cloud Resources

Example AWS:

```bash
aws ec2 describe-instances
```

---

# Terraform Best Practices

- modularize code
- use remote backend
- enable state locking
- separate environments
- avoid hardcoding
- use variables
- use outputs
- version control Terraform code

---

# Enterprise Terraform Workflow

1. Developer modifies Terraform code
2. Pull request created
3. CI validates Terraform
4. Security scans run
5. Plan generated
6. Approval required
7. Apply executed
8. Infrastructure updated

---

# 50 Terraform Interview Questions

## Beginner

1. What is Terraform?
2. What is Infrastructure as Code?
3. What is provider?
4. What is resource?
5. What is Terraform state?
6. What is backend?
7. What is variable?
8. What is output?
9. What is module?
10. What is terraform init?

---

## Intermediate

11. Difference between plan and apply?
12. What is remote backend?
13. Explain Terraform state locking.
14. What is workspace?
15. Explain Terraform lifecycle rules.
16. Difference between count and for_each?
17. What is taint?
18. Explain Terraform dependency graph.
19. What is drift detection?
20. Explain Terraform modules.

---

## Advanced

21. Explain Terraform architecture.
22. How Terraform internally works?
23. Explain Terraform providers.
24. What is Terraform graph?
25. Explain state file internals.
26. How Terraform handles dependencies?
27. Explain dynamic blocks.
28. What is Terraform Cloud?
29. Explain provider versioning.
30. What is immutable infrastructure?

---

## Production Based

31. Terraform state corruption troubleshooting.
32. Terraform state locking issue handling.
33. Resource drift investigation.
34. Terraform deployment rollback.
35. Provider authentication failure debugging.
36. Secure Terraform workflows.
37. Managing multiple environments.
38. Terraform performance optimization.
39. Infrastructure provisioning failure investigation.
40. Terraform disaster recovery strategy.

---

## Scenario Based

41. Terraform apply partially failed.
42. Resource manually deleted outside Terraform.
43. State file accidentally deleted.
44. Multiple engineers modifying infrastructure simultaneously.
45. Terraform trying to recreate production resource.
46. Provider upgrade broke infrastructure.
47. Terraform cannot connect AWS.
48. Remote backend inaccessible.
49. Infrastructure drift detected in production.
50. Explain your Terraform workflow in DevOps projects.

---

# Summary

Terraform is one of the most important Infrastructure as Code tools in DevOps.

Strong Terraform skills are essential for:
- cloud automation
- infrastructure provisioning
- Kubernetes infrastructure
- CI/CD automation
- scalable deployments
- enterprise cloud operations

Senior DevOps engineers spend significant time:
- automating infrastructure
- debugging provisioning issues
- managing state
- optimizing deployments
- securing cloud infrastructure
