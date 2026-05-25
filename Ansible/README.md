# Ansible for DevOps Engineers

# Introduction

Ansible is an open-source automation tool used for:
- configuration management
- server provisioning
- deployment automation
- orchestration
- infrastructure automation

Ansible is agentless and communicates mainly using SSH.

Organizations use Ansible for:
- patch management
- server setup
- Docker automation
- Kubernetes automation
- CI/CD integration
- cloud provisioning

---

# Why Ansible?

Before Ansible:
- manual server configuration
- inconsistent environments
- repetitive tasks
- human errors

Ansible solves:
- infrastructure consistency
- automation
- scalability
- faster provisioning

---

# Ansible Architecture

Ansible consists of:

| Component | Purpose |
|---|---|
| Control Node | machine running Ansible |
| Managed Node | target servers |
| Inventory | list of servers |
| Playbook | automation instructions |
| Module | reusable automation unit |

---

# Install Ansible

# Update Packages

Purpose:
- updates package metadata

Command:

```bash
sudo apt update
```

---

# Install Ansible

Purpose:
- installs Ansible automation engine

Command:

```bash
sudo apt install ansible -y
```

---

# Verify Installation

Purpose:
- checks Ansible version

Command:

```bash
ansible --version
```

---

# SSH Connectivity

Purpose:
- Ansible requires SSH access to servers

Test SSH:

```bash
ssh ubuntu@SERVER-IP
```

---

# Generate SSH Key

Purpose:
- passwordless authentication

Command:

```bash
ssh-keygen
```

---

# Copy SSH Key

Purpose:
- copies SSH key to target server

Command:

```bash
ssh-copy-id ubuntu@SERVER-IP
```

---

# Inventory File

Inventory stores server information.

---

# Create Inventory File

Purpose:
- defines managed servers

Command:

```bash
vim inventory
```

Example:

```ini
[web]
192.168.1.10

[db]
192.168.1.20
```

---

# Ping Managed Nodes

Purpose:
- tests Ansible connectivity

Command:

```bash
ansible all -i inventory -m ping
```

---

# Ad-hoc Commands

Ad-hoc commands execute one-time tasks.

---

# Check Uptime

Purpose:
- checks server uptime

Command:

```bash
ansible all -i inventory -a "uptime"
```

---

# Install Package

Purpose:
- installs package remotely

Command:

```bash
ansible all -i inventory -b -m apt -a "name=nginx state=present"
```

---

# Start Service

Purpose:
- starts service remotely

Command:

```bash
ansible all -i inventory -b -m service -a "name=nginx state=started"
```

---

# Copy File

Purpose:
- transfers file to servers

Command:

```bash
ansible all -i inventory -m copy -a "src=index.html dest=/var/www/html/"
```

---

# Playbooks

Playbooks automate multiple tasks.

---

# Create Playbook

Purpose:
- defines automation workflow

Command:

```bash
vim nginx.yml
```

Example:

```yaml
---
- hosts: web
  become: yes

  tasks:

    - name: Install Nginx
      apt:
        name: nginx
        state: present

    - name: Start Nginx
      service:
        name: nginx
        state: started
```

---

# Run Playbook

Purpose:
- executes automation workflow

Command:

```bash
ansible-playbook -i inventory nginx.yml
```

---

# Variables

Variables improve reusability.

Example:

```yaml
vars:
  package_name: nginx
```

---

# Handlers

Handlers execute when triggered.

Example:

```yaml
handlers:
  - name: restart nginx
    service:
      name: nginx
      state: restarted
```

---

# Roles

Roles organize Ansible code.

Benefits:
- modularization
- reusability
- scalability

---

# Create Role

Purpose:
- generates role structure

Command:

```bash
ansible-galaxy init nginx-role
```

---

# Ansible Galaxy

Galaxy provides reusable roles.

---

# Install Galaxy Role

Purpose:
- downloads community role

Command:

```bash
ansible-galaxy install geerlingguy.nginx
```

---

# Ansible Vault

Vault encrypts sensitive data.

---

# Create Encrypted File

Purpose:
- secures passwords and secrets

Command:

```bash
ansible-vault create secrets.yml
```

---

# Edit Vault File

Purpose:
- modifies encrypted file

Command:

```bash
ansible-vault edit secrets.yml
```

---

# Run Playbook with Vault

Purpose:
- decrypts secrets during execution

Command:

```bash
ansible-playbook site.yml --ask-vault-pass
```

---

# Dynamic Inventory

Dynamic inventory automatically discovers servers.

Common Providers:
- AWS
- Azure
- GCP

---

# Ansible Modules

Popular modules:
- apt
- yum
- copy
- file
- service
- shell
- command

---

# Check Syntax

Purpose:
- validates playbook syntax

Command:

```bash
ansible-playbook site.yml --syntax-check
```

---

# Dry Run

Purpose:
- previews changes without applying

Command:

```bash
ansible-playbook site.yml --check
```

---

# Verbose Output

Purpose:
- detailed troubleshooting logs

Command:

```bash
ansible-playbook site.yml -vvv
```

---

# Ansible Tags

Tags execute specific tasks.

Example:

```yaml
tags:
  - install
```

Run specific tag:

```bash
ansible-playbook site.yml --tags install
```

---

# Ansible with Docker

Ansible can:
- install Docker
- deploy containers
- manage Docker Compose

---

# Ansible with Kubernetes

Ansible can:
- deploy Kubernetes manifests
- manage clusters
- automate Helm charts

---

# Ansible Security Best Practices

- use Vault
- use SSH keys
- restrict sudo access
- avoid hardcoded passwords
- secure inventory files

---

# Troubleshooting Ansible

# Check Connectivity

Purpose:
- verifies SSH communication

Command:

```bash
ansible all -i inventory -m ping
```

---

# Validate Syntax

Purpose:
- detects YAML errors

Command:

```bash
ansible-playbook site.yml --syntax-check
```

---

# Dry Run

Purpose:
- previews execution safely

Command:

```bash
ansible-playbook site.yml --check
```

---

# Verbose Logs

Purpose:
- detailed debugging

Command:

```bash
ansible-playbook site.yml -vvv
```

---

# 50 Most Used Ansible Commands

| Command | Purpose |
|---|---|
| ansible --version | check Ansible version |
| ansible all -m ping | connectivity test |
| ansible-playbook | execute playbook |
| ansible-galaxy init | create role |
| ansible-galaxy install | install role |
| ansible-vault create | create encrypted file |
| ansible-vault edit | edit vault |
| ansible-vault view | view vault |
| ansible-vault encrypt | encrypt file |
| ansible-vault decrypt | decrypt file |
| ansible-inventory --list | inventory details |
| ansible-doc | module documentation |
| ansible-playbook --syntax-check | validate syntax |
| ansible-playbook --check | dry run |
| ansible-playbook -vvv | verbose logs |
| ansible all -a uptime | check uptime |
| ansible all -m copy | copy files |
| ansible all -m file | manage files |
| ansible all -m apt | install packages |
| ansible all -m yum | install packages |
| ansible all -m service | manage services |
| ansible all -m shell | shell commands |
| ansible all -m command | execute commands |
| ansible all -m user | manage users |
| ansible all -m group | manage groups |
| ansible all -m cron | manage cron jobs |
| ansible all -m git | clone repositories |
| ansible all -m docker_container | manage containers |
| ansible all -m kubernetes.core.k8s | manage Kubernetes |
| ansible-playbook --tags | run tags |
| ansible-playbook --limit | limit hosts |
| ansible-config dump | config details |
| ansible localhost -m setup | gather facts |
| ansible all -m reboot | reboot servers |
| ansible all -m setup | system facts |
| ansible-playbook --diff | show changes |
| ansible-playbook --step | step execution |
| ansible all -m fetch | fetch files |
| ansible all -m archive | archive files |
| ansible all -m unarchive | extract archives |
| ansible all -m systemd | manage systemd |
| ansible all -m uri | API calls |
| ansible all -m get_url | download files |
| ansible all -m lineinfile | modify lines |
| ansible all -m replace | replace text |
| ansible all -m template | Jinja2 templates |
| ansible all -m synchronize | rsync sync |
| ansible all -m hostname | manage hostname |
| ansible all -m mount | mount filesystems |
| ansible all -m selinux | manage SELinux |

---

# Real World Production Scenarios

# Scenario 1 — Playbook Failing on Production

Symptoms:
- task failure during deployment

Investigation:

```bash
ansible-playbook site.yml -vvv
```

Possible Causes:
- YAML syntax issue
- package repository failure
- SSH issue

---

# Scenario 2 — SSH Authentication Failure

Symptoms:
- UNREACHABLE errors

Investigation:
- SSH key permissions
- firewall rules
- username mismatch

---

# Scenario 3 — Idempotency Issue

Problem:
- repeated changes every run

Fix:
- use proper modules instead of shell commands

---

# Scenario 4 — Vault Password Failure

Symptoms:
- decryption failed

Investigation:
- wrong vault password
- corrupted vault file

---

# Scenario 5 — Slow Playbook Execution

Possible Causes:
- gathering facts
- serial execution
- network latency

Optimization:
- disable unnecessary facts
- parallel execution

---

# Production Troubleshooting Workflow

# Step 1 — Check Connectivity

```bash
ansible all -i inventory -m ping
```

---

# Step 2 — Validate Syntax

```bash
ansible-playbook site.yml --syntax-check
```

---

# Step 3 — Dry Run

```bash
ansible-playbook site.yml --check
```

---

# Step 4 — Enable Verbose Logs

```bash
ansible-playbook site.yml -vvv
```

---

# Step 5 — Verify SSH

```bash
ssh USER@SERVER-IP
```

---

# Step 6 — Check Inventory

```bash
ansible-inventory --list
```

---

# Enterprise Ansible Workflow

1. Developer updates playbook
2. Pull request created
3. CI validates playbook
4. Security checks run
5. Playbook tested in staging
6. Approval required
7. Production automation executed

---

# Ansible Best Practices

- use roles
- modularize playbooks
- use Vault
- avoid shell module when possible
- use idempotent tasks
- separate environments
- version control playbooks

---

# 50 Ansible Interview Questions

## Beginner

1. What is Ansible?
2. What is configuration management?
3. What is inventory?
4. What is playbook?
5. What is module?
6. What is role?
7. What is YAML?
8. What is Ansible Vault?
9. What is ad-hoc command?
10. What is idempotency?

---

## Intermediate

11. Explain Ansible architecture.
12. Difference between shell and command module?
13. What are handlers?
14. What are tags?
15. What is dynamic inventory?
16. Explain Ansible Galaxy.
17. What is become?
18. How Ansible communicates with servers?
19. Explain Ansible variables.
20. Difference between include_tasks and import_tasks?

---

## Advanced

21. Explain Ansible execution flow.
22. How Ansible ensures idempotency?
23. What are custom modules?
24. Explain Jinja2 templates.
25. What is Ansible callback plugin?
26. Explain strategy plugins.
27. How Ansible handles parallelism?
28. What is fact gathering?
29. Explain Ansible collections.
30. How to optimize Ansible performance?

---

## Production Based

31. Playbook failing in production troubleshooting.
32. SSH authentication issue debugging.
33. Vault decryption failure handling.
34. Slow playbook optimization.
35. Managing secrets securely.
36. Automating Kubernetes using Ansible.
37. Ansible CI/CD integration.
38. Handling configuration drift.
39. Scaling Ansible automation.
40. Disaster recovery using Ansible.

---

## Scenario Based

41. Inventory file accidentally corrupted.
42. Playbook works manually but fails in Jenkins.
43. Ansible unable to connect servers.
44. Playbook causing repeated changes.
45. Package installation failing on some servers.
46. Vault password lost.
47. Production deployment partially failed.
48. Dynamic inventory not discovering servers.
49. YAML syntax issue breaking pipeline.
50. Explain your Ansible automation workflow in DevOps projects.

---

# Summary

Ansible is one of the most important automation tools in DevOps.

Strong Ansible skills are essential for:
- infrastructure automation
- server management
- deployments
- CI/CD integration
- Kubernetes automation
- cloud provisioning

Senior DevOps engineers spend significant time:
- automating infrastructure
- debugging deployments
- managing configurations
- securing automation workflows
- optimizing operational efficiency
