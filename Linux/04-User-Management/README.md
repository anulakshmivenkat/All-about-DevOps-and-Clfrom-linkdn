# Linux User Management for DevOps Engineers

# Introduction

User management is one of the most critical responsibilities of a DevOps engineer.

In production environments, improper user access management can lead to:

- Security breaches
- Unauthorized access
- Data leaks
- Infrastructure compromise
- Privilege escalation attacks

Every Linux server contains:
- users
- groups
- permissions
- authentication mechanisms
- sudo access control

Understanding Linux user management is mandatory for:
- DevOps
- Cloud Engineering
- Kubernetes Administration
- Site Reliability Engineering
- Security Engineering

---

# Linux User Types

| User Type | Description |
|---|---|
| Root User | Super administrator |
| System User | Used by services |
| Regular User | Human users |
| Service Accounts | Jenkins, Docker, Kubernetes |

---

# Important User Files

| File | Purpose |
|---|---|
| /etc/passwd | User information |
| /etc/shadow | Password hashes |
| /etc/group | Group information |
| /etc/gshadow | Secure group data |
| /home | User home directories |
| /etc/sudoers | Sudo configuration |

---

# Understanding /etc/passwd

View file:

```bash
cat /etc/passwd
```

Example:

```bash
ubuntu:x:1000:1000:Ubuntu User:/home/ubuntu:/bin/bash
```

Breakdown:

| Field | Meaning |
|---|---|
| ubuntu | Username |
| x | Password placeholder |
| 1000 | UID |
| 1000 | GID |
| Ubuntu User | Comment |
| /home/ubuntu | Home directory |
| /bin/bash | Login shell |

---

# Understanding /etc/shadow

View:

```bash
sudo cat /etc/shadow
```

Contains:
- encrypted passwords
- password expiry
- password aging

Example:

```bash
ubuntu:$6$asdhasdhasd...
```

---

# User Management Commands

# Create User

```bash
sudo useradd devopsuser
```

Create with home directory:

```bash
sudo useradd -m devopsuser
```

Create with shell:

```bash
sudo useradd -m -s /bin/bash devopsuser
```

---

# Set Password

```bash
sudo passwd devopsuser
```

---

# Delete User

```bash
sudo userdel devopsuser
```

Delete with home directory:

```bash
sudo userdel -r devopsuser
```

---

# Modify User

```bash
sudo usermod -aG docker devopsuser
```

---

# Lock User

```bash
sudo passwd -l devopsuser
```

---

# Unlock User

```bash
sudo passwd -u devopsuser
```

---

# Expire User Password

```bash
sudo chage -d 0 devopsuser
```

---

# Check Password Expiry

```bash
sudo chage -l devopsuser
```

---

# Group Management Commands

# Create Group

```bash
sudo groupadd devops
```

---

# Delete Group

```bash
sudo groupdel devops
```

---

# Add User to Group

```bash
sudo usermod -aG docker ubuntu
```

---

# Remove User from Group

```bash
sudo gpasswd -d ubuntu docker
```

---

# View Groups

```bash
groups
```

---

# View User ID

```bash
id ubuntu
```

---

# Sudo Access Management

# Add User to sudo

Ubuntu:

```bash
sudo usermod -aG sudo devopsuser
```

RHEL/CentOS:

```bash
sudo usermod -aG wheel devopsuser
```

---

# Edit sudoers Safely

```bash
sudo visudo
```

Never edit /etc/sudoers directly.

---

# Example sudoers Entry

```bash
devopsuser ALL=(ALL) NOPASSWD:ALL
```

---

# SSH User Access Management

# Disable Root Login

Edit:

```bash
sudo vim /etc/ssh/sshd_config
```

Change:

```bash
PermitRootLogin no
```

Restart SSH:

```bash
sudo systemctl restart sshd
```

---

# Disable Password Authentication

```bash
PasswordAuthentication no
```

Use SSH keys instead.

---

# Generate SSH Key

```bash
ssh-keygen
```

---

# Copy SSH Key

```bash
ssh-copy-id ubuntu@server-ip
```

---

# User Monitoring Commands

# Logged in Users

```bash
who
```

---

# Last Logged Users

```bash
last
```

---

# Current User

```bash
whoami
```

---

# Check Failed Login Attempts

```bash
sudo faillog
```

---

# Check Authentication Logs

Ubuntu:

```bash
sudo tail -f /var/log/auth.log
```

RHEL:

```bash
sudo tail -f /var/log/secure
```

---

# 50 Most Used User Management Commands

```bash
whoami
who
w
id
groups
users
last
lastlog
finger
su
sudo
passwd
useradd
usermod
userdel
groupadd
groupdel
groupmod
gpasswd
newgrp
chage
chsh
chfn
vipw
vigr
visudo
faillog
passwd -S
pwck
grpck
getent passwd
getent group
logname
uname -a
hostnamectl
loginctl
sudo -l
sudo su
ssh
ssh-keygen
ssh-copy-id
scp
sftp
pkill -u
ps -u
crontab -u
chmod
chown
chgrp
umask
```

---

# Real World Production Scenarios

# Scenario 1 — Jenkins Permission Denied

Problem:

```bash
permission denied while trying to connect to Docker daemon socket
```

Root Cause:
Jenkins user not part of docker group.

Fix:

```bash
sudo usermod -aG docker jenkins
sudo systemctl restart jenkins
```

---

# Scenario 2 — SSH Access Failed

Root Causes:
- wrong permissions
- SSH service down
- wrong SSH key
- firewall issue

Troubleshooting:

```bash
systemctl status sshd
journalctl -u sshd
chmod 600 ~/.ssh/authorized_keys
```

---

# Scenario 3 — Sudden Unauthorized Access

Investigation Commands:

```bash
last
lastlog
cat /var/log/auth.log
who
w
```

---

# Security Best Practices

- Disable root login
- Use SSH keys
- Enforce MFA
- Use least privilege
- Rotate passwords
- Audit sudo access
- Remove inactive users
- Monitor auth logs
- Disable unused services

---

# Production Troubleshooting Guide

# User Cannot Run sudo

Check:

```bash
groups username
```

Fix:

```bash
sudo usermod -aG sudo username
```

---

# Home Directory Missing

Fix:

```bash
sudo mkdir /home/devopsuser
sudo chown devopsuser:devopsuser /home/devopsuser
```

---

# Account Locked

Unlock:

```bash
sudo passwd -u username
```

---

# Password Expired

Reset:

```bash
sudo passwd username
```

---

# 50 Linux User Management Interview Questions

## Beginner

1. What is UID in Linux?
2. Difference between UID and GID?
3. What is root user?
4. What is sudo?
5. Difference between su and sudo?
6. What is /etc/passwd?
7. What is /etc/shadow?
8. Why is /etc/shadow protected?
9. What is a group in Linux?
10. How to create a user?

---

## Intermediate

11. Difference between system user and regular user?
12. What is password aging?
13. Explain chage command.
14. What is SSH?
15. What are SSH keys?
16. Difference between public and private key?
17. What is visudo?
18. Why should we not edit sudoers directly?
19. What is PAM?
20. What is authentication vs authorization?

---

## Advanced

21. How to secure Linux SSH access?
22. How to disable root login?
23. What is privilege escalation?
24. Explain least privilege principle.
25. How to audit Linux user activity?
26. How to investigate failed logins?
27. What is LDAP?
28. What is Active Directory integration?
29. How does sudo internally work?
30. How to troubleshoot SSH connection issues?

---

## Production Based

31. Jenkins permission denied troubleshooting?
32. Docker socket permission issue?
33. User cannot access Kubernetes cluster?
34. Sudden root login detected?
35. How to secure production Linux servers?
36. How to rotate SSH keys?
37. How to monitor authentication logs?
38. How to disable inactive accounts?
39. What is centralized authentication?
40. How to manage thousands of users in enterprise environments?

---

## Scenario Based

41. A user accidentally deleted files. What will you do?
42. How to trace who deleted a file?
43. How to recover locked accounts?
44. User cannot execute deployment scripts.
45. SSH access suddenly stopped working.
46. Production engineer lost sudo access.
47. Unauthorized login from unknown IP.
48. Root filesystem permissions changed accidentally.
49. Multiple failed login attempts detected.
50. Explain your approach to Linux hardening.

---

# Summary

Linux user management is foundational for:
- DevOps
- Kubernetes
- Cloud Security
- CI/CD
- Production Operations

Strong Linux administration skills separate junior engineers from senior DevOps engineers.
