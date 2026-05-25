# AWS Troubleshooting and Production Debugging

# Introduction

AWS troubleshooting is a critical skill for:
- DevOps Engineers
- Cloud Engineers
- Site Reliability Engineers
- Platform Engineers

Production AWS environments fail because of:
- EC2 instance failures
- VPC networking issues
- IAM permission problems
- Route53 DNS failures
- Application Load Balancer issues
- EKS cluster failures
- Auto Scaling issues
- S3 permission errors

Strong AWS debugging skills are essential in enterprise production environments.

---

# AWS Troubleshooting Workflow

A good cloud engineer:
1. identifies symptoms
2. verifies infrastructure
3. checks permissions
4. investigates logs
5. identifies root cause
6. applies fix
7. prevents recurrence

---

# AWS Core Services

| Service | Purpose |
|---|---|
| EC2 | virtual machines |
| VPC | networking |
| IAM | access management |
| S3 | object storage |
| EKS | Kubernetes |
| Route53 | DNS |
| ALB/NLB | load balancing |
| CloudWatch | monitoring |
| Auto Scaling | scaling infrastructure |

---

# AWS CLI Configuration

# Configure AWS CLI

Purpose:
- configures AWS credentials

Command:

```bash
aws configure
```

---

# Verify AWS Identity

Purpose:
- checks current IAM identity

Command:

```bash
aws sts get-caller-identity
```

---

# EC2 Troubleshooting

EC2 issues commonly involve:
- SSH failures
- instance crashes
- networking issues
- disk exhaustion

---

# List EC2 Instances

Purpose:
- checks instance status

Command:

```bash
aws ec2 describe-instances
```

---

# Instance State

Purpose:
- verifies running state

Command:

```bash
aws ec2 describe-instance-status
```

---

# Reboot EC2 Instance

Purpose:
- restarts instance

Command:

```bash
aws ec2 reboot-instances --instance-ids INSTANCE_ID
```

---

# Start EC2 Instance

Purpose:
- starts stopped instance

Command:

```bash
aws ec2 start-instances --instance-ids INSTANCE_ID
```

---

# Stop EC2 Instance

Purpose:
- stops running instance

Command:

```bash
aws ec2 stop-instances --instance-ids INSTANCE_ID
```

---

# Security Group Troubleshooting

Security groups commonly block:
- SSH
- HTTP
- HTTPS
- database traffic

---

# List Security Groups

Purpose:
- verifies firewall rules

Command:

```bash
aws ec2 describe-security-groups
```

---

# VPC Troubleshooting

VPC issues commonly involve:
- routing problems
- NAT gateway failures
- subnet misconfiguration

---

# List VPCs

Purpose:
- checks VPC configuration

Command:

```bash
aws ec2 describe-vpcs
```

---

# Route Tables

Purpose:
- verifies routing

Command:

```bash
aws ec2 describe-route-tables
```

---

# Subnets

Purpose:
- verifies subnet configuration

Command:

```bash
aws ec2 describe-subnets
```

---

# Internet Gateway

Purpose:
- verifies internet access

Command:

```bash
aws ec2 describe-internet-gateways
```

---

# IAM Troubleshooting

IAM issues are extremely common.

Problems include:
- AccessDenied
- missing permissions
- role assumption failures

---

# List IAM Users

Purpose:
- verifies IAM users

Command:

```bash
aws iam list-users
```

---

# List IAM Roles

Purpose:
- checks IAM roles

Command:

```bash
aws iam list-roles
```

---

# Simulate IAM Policy

Purpose:
- verifies permissions

Command:

```bash
aws iam simulate-principal-policy
```

---

# S3 Troubleshooting

S3 issues commonly involve:
- AccessDenied
- bucket policy issues
- encryption problems

---

# List S3 Buckets

Purpose:
- checks buckets

Command:

```bash
aws s3 ls
```

---

# Bucket Policy

Purpose:
- verifies bucket permissions

Command:

```bash
aws s3api get-bucket-policy --bucket BUCKET_NAME
```

---

# Copy File to S3

Purpose:
- uploads objects

Command:

```bash
aws s3 cp file.txt s3://bucket-name
```

---

# Route53 Troubleshooting

DNS issues commonly cause:
- application downtime
- service failures

---

# List Hosted Zones

Purpose:
- verifies Route53 DNS

Command:

```bash
aws route53 list-hosted-zones
```

---

# DNS Record Details

Purpose:
- checks DNS records

Command:

```bash
aws route53 list-resource-record-sets --hosted-zone-id ZONE_ID
```

---

# Test DNS

Purpose:
- verifies DNS resolution

Command:

```bash
dig example.com
```

---

# Load Balancer Troubleshooting

ALB/NLB issues commonly involve:
- unhealthy targets
- security groups
- listener issues

---

# List Load Balancers

Purpose:
- checks ALB/NLB

Command:

```bash
aws elbv2 describe-load-balancers
```

---

# Target Group Health

Purpose:
- verifies backend health

Command:

```bash
aws elbv2 describe-target-health --target-group-arn TARGET_GROUP_ARN
```

---

# CloudWatch Troubleshooting

CloudWatch provides:
- metrics
- logs
- alerts

---

# List CloudWatch Alarms

Purpose:
- checks monitoring alerts

Command:

```bash
aws cloudwatch describe-alarms
```

---

# View CloudWatch Logs

Purpose:
- investigates application issues

Command:

```bash
aws logs describe-log-groups
```

---

# Auto Scaling Troubleshooting

Auto Scaling issues involve:
- scaling not triggering
- instance launch failures

---

# List Auto Scaling Groups

Purpose:
- checks scaling groups

Command:

```bash
aws autoscaling describe-auto-scaling-groups
```

---

# EKS Troubleshooting

EKS issues commonly involve:
- node failures
- networking problems
- IAM roles
- pod failures

---

# List EKS Clusters

Purpose:
- verifies EKS clusters

Command:

```bash
aws eks list-clusters
```

---

# Update kubeconfig

Purpose:
- connects kubectl to EKS

Command:

```bash
aws eks update-kubeconfig --region REGION --name CLUSTER_NAME
```

---

# Kubernetes Nodes

Purpose:
- checks EKS nodes

Command:

```bash
kubectl get nodes
```

---

# Pod Troubleshooting

Purpose:
- investigates pod failures

Command:

```bash
kubectl describe pod POD_NAME
```

---

# CloudTrail Troubleshooting

CloudTrail tracks:
- AWS API activity
- security events
- IAM activity

---

# List Trails

Purpose:
- verifies audit logging

Command:

```bash
aws cloudtrail describe-trails
```

---

# Lookup Events

Purpose:
- investigates AWS actions

Command:

```bash
aws cloudtrail lookup-events
```

---

# Production Incident Workflow

# Step 1 — Identify Symptoms

Examples:
- website unavailable
- EC2 unreachable
- EKS failing

---

# Step 2 — Verify Infrastructure

Commands:

```bash
aws ec2 describe-instances
kubectl get nodes
```

---

# Step 3 — Verify Networking

Commands:

```bash
aws ec2 describe-route-tables
aws ec2 describe-security-groups
```

---

# Step 4 — Verify Permissions

Commands:

```bash
aws sts get-caller-identity
aws iam list-roles
```

---

# Step 5 — Check Monitoring

Commands:

```bash
aws cloudwatch describe-alarms
```

---

# Step 6 — Check Logs

Commands:

```bash
aws logs describe-log-groups
kubectl logs POD_NAME
```

---

# Step 7 — Identify Root Cause

Examples:
- security group blocked
- IAM denied access
- node failure
- DNS misconfiguration

---

# Step 8 — Apply Fix

Examples:
- update security group
- fix IAM policy
- restart instances
- scale infrastructure

---

# Step 9 — Prevent Recurrence

Examples:
- monitoring
- alerting
- autoscaling
- backup strategy

---

# 100 Most Used AWS Troubleshooting Commands

| Command | Purpose |
|---|---|
| aws configure | configure AWS |
| aws sts get-caller-identity | verify identity |
| aws ec2 describe-instances | EC2 details |
| aws ec2 describe-instance-status | instance health |
| aws ec2 reboot-instances | reboot EC2 |
| aws ec2 start-instances | start EC2 |
| aws ec2 stop-instances | stop EC2 |
| aws ec2 terminate-instances | terminate EC2 |
| aws ec2 describe-security-groups | security groups |
| aws ec2 describe-vpcs | VPC details |
| aws ec2 describe-subnets | subnet details |
| aws ec2 describe-route-tables | routing |
| aws ec2 describe-network-interfaces | ENIs |
| aws ec2 describe-internet-gateways | internet gateways |
| aws ec2 describe-nat-gateways | NAT gateways |
| aws ec2 describe-volumes | EBS volumes |
| aws ec2 describe-snapshots | snapshots |
| aws s3 ls | S3 buckets |
| aws s3 cp | copy files |
| aws s3 sync | sync files |
| aws s3api get-bucket-policy | bucket policy |
| aws s3api get-bucket-acl | bucket ACL |
| aws iam list-users | IAM users |
| aws iam list-roles | IAM roles |
| aws iam list-policies | IAM policies |
| aws iam get-role | role details |
| aws iam simulate-principal-policy | test IAM |
| aws route53 list-hosted-zones | DNS zones |
| aws route53 list-resource-record-sets | DNS records |
| aws elbv2 describe-load-balancers | ALBs |
| aws elbv2 describe-target-health | target health |
| aws autoscaling describe-auto-scaling-groups | ASG details |
| aws cloudwatch describe-alarms | CloudWatch alarms |
| aws logs describe-log-groups | CloudWatch logs |
| aws cloudtrail describe-trails | audit trails |
| aws cloudtrail lookup-events | CloudTrail events |
| aws eks list-clusters | EKS clusters |
| aws eks update-kubeconfig | connect EKS |
| kubectl get pods | Kubernetes pods |
| kubectl logs | pod logs |
| kubectl describe pod | pod details |
| kubectl get nodes | cluster nodes |
| kubectl top nodes | node metrics |
| kubectl top pods | pod metrics |
| docker ps | running containers |
| docker logs | container logs |
| ping | connectivity |
| curl | API testing |
| dig | DNS lookup |
| nslookup | DNS resolution |
| traceroute | network tracing |
| tcpdump | packet capture |
| ss -tulpn | open ports |
| netstat -tulpn | network ports |
| top | CPU usage |
| htop | process monitoring |
| free -h | memory usage |
| vmstat | memory stats |
| iostat | disk I/O |
| df -h | disk usage |
| du -sh | directory size |
| lsof | open files |
| ps -ef | processes |
| journalctl | system logs |
| journalctl -u kubelet | kubelet logs |
| systemctl status | service health |
| grep | search logs |
| awk | text processing |
| sed | stream editing |
| vim | edit configs |
| cat | view files |
| less | paginated view |
| tail -f | follow logs |
| find | locate files |
| tar -xvf | extract archives |
| ssh | remote access |
| scp | secure copy |
| rsync | file sync |
| chmod | permissions |
| chown | ownership |
| env | environment variables |
| export | export variable |
| history | command history |
| crontab -l | cron jobs |
| mount | mounted disks |
| lsblk | block devices |
| fdisk -l | partitions |
| uname -a | kernel details |
| uptime | system load |
| whoami | current user |
| id | user details |
| helm list | Helm releases |
| helm rollback | rollback release |
| terraform validate | validate Terraform |
| terraform plan | preview changes |
| terraform apply | apply infrastructure |
| ansible-playbook | automation |
| git status | repository status |
| git log | commit history |
| git diff | code changes |
| git revert | rollback changes |

---

# Real World Production Scenarios

# Scenario 1 — EC2 SSH Access Failure

Possible Causes:
- wrong security group
- incorrect key
- instance unreachable

Investigation:

```bash
aws ec2 describe-security-groups
```

---

# Scenario 2 — ALB Returning 503

Possible Causes:
- unhealthy targets
- application failure
- wrong listener

Investigation:

```bash
aws elbv2 describe-target-health
```

---

# Scenario 3 — AccessDenied Error

Possible Causes:
- IAM policy missing
- role issue
- SCP restriction

Investigation:

```bash
aws iam simulate-principal-policy
```

---

# Scenario 4 — EKS Worker Nodes Not Joining

Possible Causes:
- IAM role issue
- networking problem
- bootstrap failure

Investigation:

```bash
kubectl get nodes
journalctl -u kubelet
```

---

# Scenario 5 — Route53 DNS Failure

Investigation:

```bash
dig example.com
aws route53 list-resource-record-sets
```

---

# Scenario 6 — Auto Scaling Not Launching Instances

Investigation:

```bash
aws autoscaling describe-auto-scaling-groups
```

---

# Root Cause Analysis (RCA)

Good AWS RCA includes:
- incident timeline
- impacted resources
- root cause
- resolution
- prevention strategy

---

# AWS Troubleshooting Best Practices

- enable CloudWatch monitoring
- centralize logs
- implement least privilege
- use Infrastructure as Code
- implement backups
- enable CloudTrail
- automate alerting

---

# 50 AWS Troubleshooting Interview Questions

## Beginner

1. What is AWS troubleshooting?
2. What is EC2?
3. What is IAM?
4. What is VPC?
5. What is Route53?
6. What is CloudWatch?
7. What is Auto Scaling?
8. What is security group?
9. What is subnet?
10. What is EKS?

---

## Intermediate

11. Difference between security group and NACL?
12. Explain VPC routing.
13. What causes EC2 SSH failures?
14. Explain IAM roles.
15. What is NAT Gateway?
16. Explain Route53 routing policies.
17. What is CloudTrail?
18. Explain EKS networking.
19. What is target group health check?
20. Explain Auto Scaling lifecycle.

---

## Advanced

21. Explain AWS networking internals.
22. What is VPC peering?
23. Explain Transit Gateway.
24. What is IAM policy evaluation logic?
25. Explain EKS architecture.
26. What is ENI in AWS?
27. Explain AWS load balancer types.
28. What is cross-account access?
29. Explain CloudWatch metrics internals.
30. What is AWS shared responsibility model?

---

## Production Based

31. EC2 outage investigation.
32. EKS production debugging.
33. ALB 503 troubleshooting.
34. Route53 DNS outage handling.
35. IAM AccessDenied investigation.
36. CloudWatch alert investigation.
37. VPC networking troubleshooting.
38. Auto Scaling debugging.
39. Production cloud incident response.
40. AWS infrastructure optimization.

---

## Scenario Based

41. Entire application unavailable.
42. EKS nodes NotReady.
43. ALB unhealthy targets.
44. EC2 disk full.
45. Route53 records missing.
46. S3 bucket inaccessible.
47. IAM role assumption failing.
48. Auto Scaling not scaling.
49. Kubernetes pods unreachable on EKS.
50. Explain your AWS production debugging workflow.

---

# Summary

AWS troubleshooting is one of the most important real-world cloud engineering skills.

Strong AWS debugging skills are essential for:
- cloud reliability
- incident response
- production operations
- infrastructure debugging
- enterprise cloud engineering

Senior DevOps engineers spend significant time:
- debugging AWS infrastructure
- investigating outages
- analyzing permissions
- fixing networking
- improving reliability
