# Shell Scripting for DevOps Engineers

# Introduction

Shell scripting is the foundation of DevOps automation.

Almost every DevOps tool internally relies on scripts.

Examples:
- Jenkins pipelines
- Kubernetes init scripts
- Terraform provisioning
- Docker entrypoints
- CI/CD automation
- Monitoring scripts
- Backup scripts

DevOps engineers use shell scripting for:
- automation
- deployment
- troubleshooting
- monitoring
- infrastructure operations

---

# What is Shell Scripting?

A shell script is a file containing Linux commands executed sequentially.

Example:

```bash
#!/bin/bash

echo "Hello DevOps"
```

---

# Script Execution Flow

1. Shell reads script
2. Executes commands line by line
3. Returns output

---

# Types of Shells

| Shell | Description |
|---|---|
| bash | Most common |
| sh | Bourne shell |
| zsh | Advanced shell |
| ksh | Korn shell |

---

# Creating Script

Create file:

```bash
vim hello.sh
```

Add:

```bash
#!/bin/bash

echo "Hello World"
```

---

# Make Script Executable

```bash
chmod +x hello.sh
```

Run:

```bash
./hello.sh
```

---

# Variables

Define variable:

```bash
name="DevOps"
```

Access variable:

```bash
echo $name
```

---

# System Variables

```bash
echo $HOME
echo $USER
echo $PATH
echo $HOSTNAME
```

---

# User Input

```bash
read -p "Enter Name: " name

echo $name
```

---

# Conditional Statements

# if Statement

```bash
if [ $a -eq $b ]
then
    echo "Equal"
fi
```

---

# if else

```bash
if [ $num -gt 10 ]
then
    echo "Greater"
else
    echo "Smaller"
fi
```

---

# Nested if

```bash
if [ $num -gt 0 ]
then
    if [ $num -lt 100 ]
    then
        echo "Valid"
    fi
fi
```

---

# Loops

# for Loop

```bash
for i in {1..5}
do
    echo $i
done
```

---

# while Loop

```bash
count=1

while [ $count -le 5 ]
do
    echo $count
    ((count++))
done
```

---

# until Loop

```bash
count=1

until [ $count -gt 5 ]
do
    echo $count
    ((count++))
done
```

---

# Functions

```bash
function greet() {
    echo "Hello DevOps"
}

greet
```

---

# Arrays

```bash
tools=("Docker" "Kubernetes" "Jenkins")

echo ${tools[0]}
```

---

# Command Line Arguments

```bash
echo $1
echo $2
```

Run:

```bash
./script.sh Docker Kubernetes
```

---

# Exit Status

```bash
echo $?
```

0 = success

Non-zero = failure

---

# Logical Operators

AND:

```bash
&&
```

OR:

```bash
||
```

---

# File Handling

Check file exists:

```bash
if [ -f file.txt ]
then
    echo "Exists"
fi
```

---

# Directory Handling

```bash
if [ -d project ]
then
    echo "Directory exists"
fi
```

---

# String Operations

```bash
name="devops"

echo ${#name}
```

---

# Arithmetic Operations

```bash
a=10
b=20

sum=$((a+b))

echo $sum
```

---

# Process Automation

Example:

```bash
#!/bin/bash

systemctl restart nginx
systemctl status nginx
```

---

# Log Cleanup Script

```bash
#!/bin/bash

find /var/log -type f -name "*.log" -mtime +7 -delete
```

---

# Backup Script

```bash
#!/bin/bash

tar -czvf backup.tar.gz /data
```

---

# Health Check Script

```bash
#!/bin/bash

df -h
free -h
uptime
```

---

# Docker Cleanup Script

```bash
#!/bin/bash

docker system prune -af
```

---

# Kubernetes Automation Script

```bash
#!/bin/bash

kubectl get pods
kubectl get nodes
kubectl get svc
```

---

# AWS Automation Script

```bash
#!/bin/bash

aws s3 ls
aws ec2 describe-instances
```

---

# Cron Jobs

Edit cron:

```bash
crontab -e
```

Example:

```bash
0 2 * * * /home/ubuntu/backup.sh
```

---

# Script Debugging

Enable debugging:

```bash
bash -x script.sh
```

---

# Error Handling

```bash
set -e
```

Stop script on errors.

---

# Strict Mode

```bash
set -euo pipefail
```

---

# Logging in Scripts

```bash
echo "Deployment Started" >> deploy.log
```

---

# Best Practices

- use meaningful variable names
- use functions
- validate inputs
- handle errors
- avoid hardcoding
- use logging
- use comments
- use strict mode

---

# Security Best Practices

- avoid plain text passwords
- use environment variables
- validate user input
- restrict script permissions
- avoid running as root

---

# 50 Most Used Shell Scripting Commands

```bash
echo
read
printf
cat
grep
awk
sed
cut
tr
sort
uniq
head
tail
find
xargs
tee
wc
chmod
chown
basename
dirname
date
sleep
expr
test
seq
curl
wget
tar
gzip
zip
unzip
scp
ssh
rsync
systemctl
journalctl
ps
top
df -h
du -sh
free -h
uptime
kill
pkill
nohup
crontab
env
export
source
alias
```

---

# Real World Production Scenarios

# Scenario 1 — Disk Cleanup Automation

Problem:
Servers running out of storage.

Solution:

```bash
find /var/log -type f -mtime +15 -delete
```

Automated using cron.

---

# Scenario 2 — CI/CD Deployment Script

Script:

```bash
#!/bin/bash

git pull

docker build -t app .

docker-compose down

docker-compose up -d
```

---

# Scenario 3 — Kubernetes Health Monitoring

```bash
#!/bin/bash

kubectl get nodes

kubectl get pods --all-namespaces
```

---

# Scenario 4 — Auto Restart Failed Service

```bash
#!/bin/bash

systemctl is-active nginx

if [ $? -ne 0 ]
then
    systemctl restart nginx
fi
```

---

# Scenario 5 — AWS Snapshot Automation

```bash
#!/bin/bash

aws ec2 create-snapshot --volume-id vol-id
```

---

# Production Troubleshooting Workflow

# Step 1 — Enable Debugging

```bash
bash -x script.sh
```

---

# Step 2 — Check Exit Status

```bash
echo $?
```

---

# Step 3 — Validate Variables

```bash
echo $variable
```

---

# Step 4 — Check Logs

```bash
cat script.log
```

---

# Step 5 — Verify Permissions

```bash
ls -l script.sh
```

---

# Common Shell Script Errors

| Error | Cause |
|---|---|
| Permission denied | missing execute permission |
| command not found | package missing |
| syntax error | bad syntax |
| variable empty | undefined variable |
| file not found | wrong path |

---

# Advanced Shell Concepts

- subshells
- pipes
- redirection
- process substitution
- traps
- signals
- named pipes
- job control

---

# Redirection

Overwrite:

```bash
>
```

Append:

```bash
>>
```

Error redirect:

```bash
2>
```

---

# Pipes

```bash
cat file.txt | grep error
```

---

# Environment Variables

Export variable:

```bash
export ENV=production
```

---

# Trap Signals

```bash
trap "echo Exiting" EXIT
```

---

# 50 Shell Scripting Interview Questions

## Beginner

1. What is shell scripting?
2. Difference between bash and sh?
3. What is shebang?
4. How to execute script?
5. What are variables?
6. Difference between local and environment variables?
7. What is exit code?
8. What is cron job?
9. Difference between > and >>?
10. What is pipe?

---

## Intermediate

11. Difference between $@ and $*?
12. What is awk?
13. What is sed?
14. Difference between grep and egrep?
15. Explain file descriptors.
16. What is xargs?
17. What is trap in shell?
18. Explain subshell.
19. What is process substitution?
20. Difference between source and bash?

---

## Advanced

21. Explain set -euo pipefail.
22. How to debug shell scripts?
23. What is race condition in scripts?
24. How to handle signals?
25. Explain named pipes.
26. What is exec command?
27. Difference between shell and kernel?
28. Explain command substitution.
29. How shell handles processes?
30. Explain shell expansion.

---

## Production Based

31. How to automate log cleanup?
32. CI/CD deployment script design?
33. Kubernetes health check automation?
34. How to secure shell scripts?
35. Script failing in cron but working manually.
36. Automating AWS backups.
37. Monitoring server health using scripts.
38. Docker cleanup automation.
39. Script performance optimization.
40. Handling production deployment failures.

---

## Scenario Based

41. Script suddenly stopped working.
42. Cron job not executing.
43. Deployment script partially failed.
44. Variable not getting exported.
45. Application restart automation failed.
46. Backup script corrupted data.
47. Jenkins shell script failing.
48. Kubernetes script timeout issue.
49. AWS CLI script authentication failed.
50. Explain your debugging process for broken scripts.

---

# Summary

Shell scripting is one of the most practical DevOps skills.

Senior DevOps engineers automate:
- deployments
- monitoring
- backups
- Kubernetes operations
- cloud infrastructure
- CI/CD workflows
- server maintenance

Strong shell scripting skills dramatically improve:
- productivity
- reliability
- operational efficiency
- incident response
