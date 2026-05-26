# Python for DevOps Engineers

# Introduction

Python is widely used in DevOps because it:
- automates repetitive tasks
- integrates with cloud APIs
- manages infrastructure
- simplifies scripting
- works well with Linux

Python is heavily used in:
- AWS automation
- Kubernetes automation
- CI/CD pipelines
- monitoring
- security tooling
- AIOps
- MLOps

---

# Why DevOps Engineers Need Python

DevOps engineers use Python for:
- automation
- scalability
- infrastructure management
- cloud orchestration
- deployment scripting
- monitoring systems

Without automation:
- infrastructure becomes difficult to manage
- repetitive tasks increase
- human errors increase

---

# Install Python

# Verify Python

Purpose:
- checks Python installation

Command:

```bash
python3 --version
```

---

# Install Python on Ubuntu

Purpose:
- installs Python

Command:

```bash
sudo apt update
sudo apt install python3 -y
```

---

# Install pip

Purpose:
- Python package manager

Command:

```bash
sudo apt install python3-pip -y
```

---

# Verify pip

Purpose:
- checks pip installation

Command:

```bash
pip3 --version
```

---

# Create Python File

Purpose:
- create script

Command:

```bash
vim app.py
```

---

# First Python Script

Example:

```python
print("Hello DevOps")
```

Run:

```bash
python3 app.py
```

---

# Python Variables

Example:

```python
name = "DevOps"
version = 3
```

---

# Python Data Types

| Type | Example |
|---|---|
| String | "hello" |
| Integer | 10 |
| Float | 5.5 |
| Boolean | True |
| List | [1,2,3] |
| Dictionary | {"name":"aws"} |

---

# Python Lists

Example:

```python
tools = ["Docker", "Kubernetes", "Terraform"]

print(tools)
```

---

# Python Dictionary

Example:

```python
cloud = {
    "provider": "AWS",
    "service": "EC2"
}

print(cloud)
```

---

# Python Conditions

Example:

```python
cpu = 90

if cpu > 80:
    print("High CPU Usage")
```

---

# Python Loops

Example:

```python
for tool in ["Docker", "Jenkins", "Kubernetes"]:
    print(tool)
```

---

# Python Functions

Example:

```python
def deploy():
    print("Deploying Application")

deploy()
```

---

# Python File Handling

# Write File

Purpose:
- writes logs/configuration

Example:

```python
with open("log.txt", "w") as file:
    file.write("Deployment Success")
```

---

# Read File

Purpose:
- reads configuration/logs

Example:

```python
with open("log.txt", "r") as file:
    print(file.read())
```

---

# Exception Handling

Purpose:
- handles failures safely

Example:

```python
try:
    print(10/0)

except Exception as e:
    print(e)
```

---

# Python Modules

Purpose:
- reusable code

Example:

```python
import os
import sys
```

---

# Useful Python Modules for DevOps

| Module | Purpose |
|---|---|
| os | operating system |
| subprocess | run shell commands |
| requests | API calls |
| boto3 | AWS automation |
| paramiko | SSH automation |
| kubernetes | Kubernetes automation |
| json | JSON processing |
| yaml | YAML processing |

---

# Run Linux Commands Using Python

Purpose:
- automation

Example:

```python
import subprocess

subprocess.run(["ls", "-l"])
```

---

# Capture Command Output

Example:

```python
import subprocess

output = subprocess.check_output(["uptime"])

print(output.decode())
```

---

# Python Automation Example

# Disk Usage Monitoring

Purpose:
- monitor server disk usage

Example:

```python
import shutil

disk = shutil.disk_usage("/")

print("Total:", disk.total)
print("Used:", disk.used)
print("Free:", disk.free)
```

---

# CPU Monitoring

Purpose:
- monitor CPU

Install package:

```bash
pip3 install psutil
```

Example:

```python
import psutil

print(psutil.cpu_percent())
```

---

# Memory Monitoring

Example:

```python
import psutil

print(psutil.virtual_memory())
```

---

# Process Monitoring

Example:

```python
import psutil

for process in psutil.process_iter():
    print(process.name())
```

---

# AWS Automation Using Python

# Install boto3

Purpose:
- AWS SDK

Command:

```bash
pip3 install boto3
```

---

# List S3 Buckets

Example:

```python
import boto3

s3 = boto3.client("s3")

response = s3.list_buckets()

for bucket in response["Buckets"]:
    print(bucket["Name"])
```

---

# Launch EC2 Instance

Example:

```python
import boto3

ec2 = boto3.resource("ec2")

ec2.create_instances(
    ImageId='ami-123456',
    MinCount=1,
    MaxCount=1,
    InstanceType='t2.micro'
)
```

---

# Kubernetes Automation Using Python

# Install Kubernetes Client

Purpose:
- Kubernetes automation

Command:

```bash
pip3 install kubernetes
```

---

# List Kubernetes Pods

Example:

```python
from kubernetes import client, config

config.load_kube_config()

v1 = client.CoreV1Api()

pods = v1.list_pod_for_all_namespaces()

for pod in pods.items:
    print(pod.metadata.name)
```

---

# Docker Automation Using Python

# Install Docker SDK

Purpose:
- Docker automation

Command:

```bash
pip3 install docker
```

---

# List Docker Containers

Example:

```python
import docker

client = docker.from_env()

containers = client.containers.list()

for container in containers:
    print(container.name)
```

---

# Jenkins Automation

# Install Jenkins Python SDK

Command:

```bash
pip3 install python-jenkins
```

---

# Connect to Jenkins

Example:

```python
import jenkins

server = jenkins.Jenkins(
    'http://localhost:8080',
    username='admin',
    password='password'
)

print(server.get_jobs())
```

---

# API Calls Using Requests

# Install Requests

Command:

```bash
pip3 install requests
```

---

# API Request Example

Example:

```python
import requests

response = requests.get("https://api.github.com")

print(response.status_code)
```

---

# JSON Parsing

Example:

```python
import json

data = '{"tool":"Docker"}'

parsed = json.loads(data)

print(parsed["tool"])
```

---

# YAML Parsing

# Install PyYAML

Command:

```bash
pip3 install pyyaml
```

---

# YAML Example

Example:

```python
import yaml

with open("config.yaml") as file:
    config = yaml.safe_load(file)

print(config)
```

---

# Virtual Environment

Purpose:
- isolate dependencies

Create:

```bash
python3 -m venv venv
```

Activate:

```bash
source venv/bin/activate
```

Deactivate:

```bash
deactivate
```

---

# Logging in Python

Purpose:
- production logging

Example:

```python
import logging

logging.basicConfig(level=logging.INFO)

logging.info("Deployment Started")
```

---

# Multithreading

Purpose:
- parallel execution

Example:

```python
import threading

def task():
    print("Running")

thread = threading.Thread(target=task)

thread.start()
```

---

# Scheduling Jobs

Purpose:
- task automation

Example:

```python
import schedule
import time

def job():
    print("Running Job")

schedule.every(10).seconds.do(job)

while True:
    schedule.run_pending()
    time.sleep(1)
```

---

# Real World DevOps Python Use Cases

| Use Case | Purpose |
|---|---|
| EC2 automation | cloud provisioning |
| Kubernetes automation | cluster management |
| Jenkins integration | CI/CD automation |
| Monitoring scripts | server health |
| Security scanning | compliance |
| Log parsing | observability |
| Alert automation | notifications |
| Backup automation | disaster recovery |

---

# Production Python Best Practices

- use virtual environments
- implement logging
- use exception handling
- avoid hardcoded secrets
- validate inputs
- modularize scripts
- use requirements.txt
- use environment variables

---

# requirements.txt

Purpose:
- dependency management

Example:

```text
boto3
requests
psutil
kubernetes
docker
```

Install:

```bash
pip3 install -r requirements.txt
```

---

# Common Python Errors in DevOps

| Error | Cause |
|---|---|
| ModuleNotFoundError | package missing |
| PermissionError | insufficient permissions |
| ConnectionError | API/network issue |
| YAML parsing error | invalid YAML |
| JSON decode error | invalid JSON |

---

# Python Troubleshooting

# Check Installed Packages

Purpose:
- verify dependencies

Command:

```bash
pip3 list
```

---

# Verify Virtual Environment

Purpose:
- environment troubleshooting

Command:

```bash
which python3
```

---

# Debug Python Script

Purpose:
- verbose debugging

Command:

```bash
python3 -m pdb app.py
```

---

# Check Logs

Purpose:
- production debugging

Command:

```bash
tail -f app.log
```

---

# Real World Python DevOps Project

# Automated EC2 Health Monitoring

Workflow:
1. Python script checks EC2 health
2. CloudWatch metrics analyzed
3. Alert sent to Slack/Email
4. Failed instances restarted automatically

Tools:
- Python
- boto3
- CloudWatch
- SNS

---

# 100 Most Used Python for DevOps Commands

| Command | Purpose |
|---|---|
| python3 --version | check Python |
| pip3 --version | check pip |
| pip3 install | install package |
| pip3 uninstall | remove package |
| pip3 list | installed packages |
| pip3 freeze | export dependencies |
| python3 app.py | run script |
| python3 -m venv | virtual environment |
| source venv/bin/activate | activate venv |
| deactivate | deactivate venv |
| pip3 install boto3 | AWS SDK |
| pip3 install requests | API library |
| pip3 install kubernetes | Kubernetes SDK |
| pip3 install docker | Docker SDK |
| pip3 install psutil | system monitoring |
| pip3 install pyyaml | YAML parsing |
| pip3 install python-jenkins | Jenkins SDK |
| pip3 install schedule | job scheduling |
| pip3 install flask | web framework |
| pip3 install fastapi | API framework |
| pip3 install pandas | data processing |
| pip3 install numpy | numerical computing |
| pip3 install matplotlib | visualization |
| python3 -m pdb | debugger |
| which python3 | Python path |
| which pip3 | pip path |
| env | environment variables |
| export | export variable |
| vim app.py | edit script |
| cat app.py | view script |
| less app.py | paginated view |
| tail -f app.log | follow logs |
| chmod +x app.py | executable script |
| ./app.py | run executable |
| crontab -e | schedule jobs |
| systemctl status | service health |
| journalctl -u | service logs |
| docker ps | containers |
| docker logs | container logs |
| kubectl get pods | Kubernetes pods |
| kubectl logs | pod logs |
| aws s3 ls | S3 buckets |
| aws ec2 describe-instances | EC2 details |
| git clone | clone repo |
| git pull | latest changes |
| git push | upload changes |
| grep | search text |
| awk | text processing |
| sed | stream editing |
| find | locate files |
| curl | API requests |
| ping | connectivity |
| netstat -tulpn | open ports |
| ss -tulpn | sockets |
| ps -ef | processes |
| top | CPU usage |
| htop | process monitor |
| free -h | memory usage |
| df -h | disk usage |
| du -sh | directory size |
| iostat | disk I/O |
| vmstat | memory stats |
| uname -a | kernel details |
| uptime | system load |
| lsblk | block devices |
| mount | mounted disks |
| chmod | permissions |
| chown | ownership |
| tar -xvf | extract archives |
| zip | compress files |
| unzip | extract zip |
| ssh | remote login |
| scp | secure copy |
| rsync | synchronization |
| systemctl restart | restart service |
| kubectl exec -it | shell access |
| docker exec -it | shell access |
| helm list | Helm releases |
| terraform init | initialize |
| terraform apply | deploy |
| ansible-playbook | automation |
| kubectl describe pod | pod details |
| kubectl get events | events |
| docker inspect | container details |
| docker images | local images |
| kubectl top nodes | node metrics |
| kubectl top pods | pod metrics |
| aws configure | AWS credentials |
| aws sts get-caller-identity | verify IAM |
| python3 -c | inline execution |
| history | command history |
| clear | clear terminal |
| pwd | current directory |
| ls -l | list files |
| mkdir | create directory |
| rm -rf | remove directory |
| cp | copy files |
| mv | move files |
| touch | create file |
| echo | output text |
| tee | write output |
| hostname | server hostname |
| hostnamectl | hostname details |

---

# 50 Python for DevOps Interview Questions with Answers

# 1. Why is Python used in DevOps?

Answer:

Python is used because it:
- simplifies automation
- integrates with APIs
- supports cloud SDKs
- works well with Linux systems

---

# 2. What is boto3?

Answer:

boto3 is AWS SDK for Python used to automate AWS services.

---

# 3. What is virtual environment?

Answer:

A virtual environment isolates Python dependencies per project.

---

# 4. Difference between list and dictionary?

Answer:

List:
- ordered collection

Dictionary:
- key-value pairs

---

# 5. What is exception handling?

Answer:

Exception handling prevents script crashes by managing runtime errors safely.

---

# 6. What is requests module?

Answer:

requests module is used for API communication and HTTP requests.

---

# 7. What is subprocess module?

Answer:

subprocess executes Linux commands from Python scripts.

---

# 8. What is YAML parsing?

Answer:

YAML parsing reads Kubernetes and configuration YAML files programmatically.

---

# 9. How do you automate AWS using Python?

Answer:

Using boto3 SDK to:
- create EC2
- manage S3
- configure IAM
- automate cloud infrastructure

---

# 10. How do you troubleshoot Python automation failures?

Answer:

Check:
- logs
- dependencies
- permissions
- network connectivity
- API authentication

Commands:

```bash
pip3 list
python3 -m pdb app.py
tail -f app.log
```

---

# Summary

Python is essential for modern DevOps because it enables:
- automation
- cloud integration
- monitoring
- infrastructure management
- CI/CD orchestration

Strong Python knowledge significantly improves:
- DevOps engineering skills
- automation capability
- cloud engineering productivity
- platform engineering expertise
