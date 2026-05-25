# Linux Troubleshooting and Production Debugging for DevOps Engineers

# Introduction

Linux troubleshooting is a core skill for:
- DevOps Engineers
- Cloud Engineers
- Site Reliability Engineers
- Platform Engineers

Production systems fail because of:
- CPU exhaustion
- memory leaks
- disk issues
- network failures
- application crashes
- Kubernetes problems
- Docker failures
- cloud infrastructure issues

The ability to debug systems quickly is one of the most valuable real-world skills.

---

# Production Troubleshooting Mindset

Never randomly restart services immediately.

A good DevOps engineer:
1. investigates symptoms
2. identifies root cause
3. collects logs
4. verifies impact
5. implements fix
6. prevents recurrence

---

# Linux System Investigation Workflow

| Step | Purpose |
|---|---|
| Check uptime | verify system load |
| Check CPU | identify high utilization |
| Check memory | identify memory pressure |
| Check disk | identify storage issues |
| Check network | verify connectivity |
| Check logs | identify errors |
| Check services | verify service health |

---

# CPU Troubleshooting

High CPU causes:
- runaway processes
- infinite loops
- traffic spikes
- bad application code

---

# Check CPU Usage

Purpose:
- displays CPU utilization

Command:

```bash
top
```

---

# Interactive Process Monitoring

Purpose:
- advanced real-time monitoring

Command:

```bash
htop
```

---

# CPU Statistics

Purpose:
- detailed CPU metrics

Command:

```bash
mpstat
```

---

# View Process CPU Usage

Purpose:
- identifies CPU-heavy processes

Command:

```bash
ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%cpu
```

---

# Memory Troubleshooting

Memory problems cause:
- application crashes
- OOM kills
- system slowness

---

# Check Memory Usage

Purpose:
- displays RAM usage

Command:

```bash
free -h
```

---

# Virtual Memory Statistics

Purpose:
- analyzes memory pressure

Command:

```bash
vmstat
```

---

# Check OOM Kills

Purpose:
- identifies memory exhaustion

Command:

```bash
dmesg | grep -i oom
```

---

# Top Memory Processes

Purpose:
- identifies memory-consuming processes

Command:

```bash
ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%mem
```

---

# Disk Troubleshooting

Disk issues cause:
- application failures
- database crashes
- Kubernetes pod failures

---

# Disk Usage

Purpose:
- displays filesystem usage

Command:

```bash
df -h
```

---

# Directory Size

Purpose:
- identifies large directories

Command:

```bash
du -sh *
```

---

# Disk Performance

Purpose:
- analyzes disk I/O

Command:

```bash
iostat
```

---

# Find Large Files

Purpose:
- identifies storage-consuming files

Command:

```bash
find / -type f -size +500M
```

---

# Network Troubleshooting

Network issues are common in:
- Kubernetes
- cloud environments
- microservices

---

# Check Connectivity

Purpose:
- tests reachability

Command:

```bash
ping google.com
```

---

# DNS Resolution

Purpose:
- verifies DNS functionality

Command:

```bash
nslookup google.com
```

---

# Advanced DNS Lookup

Purpose:
- detailed DNS investigation

Command:

```bash
dig google.com
```

---

# View Listening Ports

Purpose:
- identifies open services

Command:

```bash
ss -tulpn
```

---

# Network Connections

Purpose:
- displays active connections

Command:

```bash
netstat -tulpn
```

---

# Trace Network Route

Purpose:
- identifies routing issues

Command:

```bash
traceroute google.com
```

---

# Capture Packets

Purpose:
- analyzes network traffic

Command:

```bash
tcpdump -i eth0
```

---

# Logs Troubleshooting

Logs are critical during incidents.

---

# View System Logs

Purpose:
- displays systemd logs

Command:

```bash
journalctl
```

---

# Follow Logs Live

Purpose:
- real-time log monitoring

Command:

```bash
journalctl -f
```

---

# Service Logs

Purpose:
- investigates specific service

Command:

```bash
journalctl -u nginx
```

---

# Kernel Logs

Purpose:
- kernel-level investigation

Command:

```bash
dmesg
```

---

# View File Logs

Purpose:
- checks application logs

Command:

```bash
tail -f /var/log/syslog
```

---

# Search Logs

Purpose:
- finds errors

Command:

```bash
grep -i error /var/log/syslog
```

---

# Service Troubleshooting

---

# Check Service Status

Purpose:
- verifies service health

Command:

```bash
systemctl status nginx
```

---

# Restart Service

Purpose:
- restarts failed service

Command:

```bash
systemctl restart nginx
```

---

# Start Service

Purpose:
- starts stopped service

Command:

```bash
systemctl start nginx
```

---

# Stop Service

Purpose:
- stops running service

Command:

```bash
systemctl stop nginx
```

---

# Enable Service

Purpose:
- auto-start on boot

Command:

```bash
systemctl enable nginx
```

---

# Docker Troubleshooting

Container issues include:
- crashes
- networking issues
- image failures

---

# Running Containers

Purpose:
- lists active containers

Command:

```bash
docker ps
```

---

# Container Logs

Purpose:
- investigates container failures

Command:

```bash
docker logs CONTAINER_ID
```

---

# Container Resource Usage

Purpose:
- monitors container performance

Command:

```bash
docker stats
```

---

# Enter Container

Purpose:
- interactive container shell

Command:

```bash
docker exec -it CONTAINER_ID bash
```

---

# Kubernetes Troubleshooting

Kubernetes troubleshooting is critical in production.

---

# List Pods

Purpose:
- checks pod status

Command:

```bash
kubectl get pods -A
```

---

# Describe Pod

Purpose:
- detailed pod investigation

Command:

```bash
kubectl describe pod POD_NAME
```

---

# Pod Logs

Purpose:
- investigates application failures

Command:

```bash
kubectl logs POD_NAME
```

---

# Node Status

Purpose:
- checks Kubernetes nodes

Command:

```bash
kubectl get nodes
```

---

# Node Resource Usage

Purpose:
- identifies overloaded nodes

Command:

```bash
kubectl top nodes
```

---

# Pod Resource Usage

Purpose:
- identifies heavy workloads

Command:

```bash
kubectl top pods
```

---

# Production Incident Workflow

# Step 1 — Identify Symptoms

Examples:
- website down
- API slow
- Kubernetes pods crashing

---

# Step 2 — Check Infrastructure

Commands:

```bash
top
free -h
df -h
```

---

# Step 3 — Check Logs

Commands:

```bash
journalctl -f
kubectl logs
docker logs
```

---

# Step 4 — Verify Networking

Commands:

```bash
ping
curl
dig
```

---

# Step 5 — Identify Root Cause

Examples:
- memory exhaustion
- disk full
- DNS failure
- application bug

---

# Step 6 — Apply Fix

Examples:
- restart service
- free storage
- scale infrastructure
- rollback deployment

---

# Step 7 — Prevent Recurrence

Examples:
- monitoring
- alerts
- scaling
- optimization

---

# Performance Troubleshooting

---

# System Load

Purpose:
- checks system pressure

Command:

```bash
uptime
```

---

# Process Tree

Purpose:
- process hierarchy

Command:

```bash
pstree
```

---

# Open Files

Purpose:
- identifies file handles

Command:

```bash
lsof
```

---

# Real-Time I/O Monitoring

Purpose:
- disk activity analysis

Command:

```bash
iotop
```

---

# Network Bandwidth

Purpose:
- network throughput monitoring

Command:

```bash
iftop
```

---

# 100 Most Used Linux Troubleshooting Commands

| Command | Purpose |
|---|---|
| top | CPU monitoring |
| htop | advanced monitoring |
| free -h | memory usage |
| vmstat | virtual memory |
| iostat | disk I/O |
| df -h | disk usage |
| du -sh | directory size |
| ps -ef | running processes |
| ps aux | process list |
| pstree | process hierarchy |
| kill | terminate process |
| killall | terminate by name |
| pkill | process kill |
| systemctl status | service status |
| systemctl restart | restart service |
| journalctl | system logs |
| journalctl -f | live logs |
| dmesg | kernel logs |
| tail -f | follow logs |
| grep | search logs |
| awk | text processing |
| sed | stream editing |
| find | locate files |
| locate | fast search |
| lsof | open files |
| ss -tulpn | listening ports |
| netstat -tulpn | network ports |
| ping | connectivity |
| traceroute | network path |
| tcpdump | packet capture |
| curl | API testing |
| wget | download |
| dig | DNS lookup |
| nslookup | DNS testing |
| host | hostname lookup |
| ip addr | IP details |
| ip route | routing table |
| route -n | routes |
| arp -a | ARP table |
| uname -a | kernel details |
| uptime | system load |
| who | logged users |
| whoami | current user |
| id | user details |
| chmod | permissions |
| chown | ownership |
| mount | mounted disks |
| umount | unmount disks |
| fdisk -l | disk partitions |
| lsblk | block devices |
| blkid | filesystem UUID |
| crontab -l | cron jobs |
| crontab -e | edit cron |
| env | environment |
| export | export variable |
| printenv | environment variables |
| history | command history |
| alias | command aliases |
| source | reload shell |
| vim | text editor |
| cat | display files |
| less | paginated view |
| more | file view |
| head | first lines |
| tail | last lines |
| wc -l | line count |
| sort | sorting |
| uniq | unique lines |
| cut | column extraction |
| xargs | argument passing |
| tee | redirect output |
| nohup | background process |
| screen | terminal session |
| tmux | terminal multiplexer |
| tar -xvf | extract archive |
| tar -czvf | compress archive |
| gzip | compression |
| gunzip | decompression |
| zip | create zip |
| unzip | extract zip |
| scp | secure copy |
| rsync | sync files |
| ssh | remote access |
| ssh-keygen | generate SSH key |
| chmod 600 | secure SSH key |
| docker ps | running containers |
| docker logs | container logs |
| docker stats | container metrics |
| docker exec | enter container |
| kubectl get pods | Kubernetes pods |
| kubectl describe pod | pod details |
| kubectl logs | pod logs |
| kubectl top nodes | node metrics |
| kubectl get events | cluster events |
| kubectl describe node | node details |
| kubectl exec | pod shell |
| aws sts get-caller-identity | verify AWS |
| aws ec2 describe-instances | EC2 details |
| terraform validate | validate IaC |
| ansible-playbook | automation |
| helm list | Helm releases |
| helm upgrade | upgrade release |

---

# Real World Production Scenarios

# Scenario 1 — Linux Server Extremely Slow

Investigation:

```bash
top
htop
iostat
vmstat
```

Possible Causes:
- CPU exhaustion
- memory pressure
- disk bottleneck

---

# Scenario 2 — Disk Full

Symptoms:
- application crashes
- pods failing

Investigation:

```bash
df -h
du -sh *
find / -type f -size +1G
```

---

# Scenario 3 — Kubernetes Pod CrashLoopBackOff

Investigation:

```bash
kubectl describe pod POD_NAME
kubectl logs POD_NAME
```

Possible Causes:
- application crash
- missing environment variable
- image pull issue

---

# Scenario 4 — Docker Container Exiting

Investigation:

```bash
docker logs CONTAINER_ID
docker inspect CONTAINER_ID
```

---

# Scenario 5 — High Network Latency

Investigation:

```bash
ping
traceroute
tcpdump
```

---

# Scenario 6 — Memory Leak

Symptoms:
- increasing RAM usage

Investigation:

```bash
top
free -h
ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%mem
```

---

# Root Cause Analysis (RCA)

RCA identifies:
- why incident occurred
- how to prevent recurrence

Good RCA includes:
- timeline
- root cause
- impact
- fix
- prevention plan

---

# Incident Response Best Practices

- stay calm
- collect logs first
- avoid random restarts
- communicate clearly
- document investigation
- implement monitoring

---

# Linux Troubleshooting Best Practices

- monitor systems continuously
- centralize logs
- implement alerting
- automate health checks
- maintain backups
- test disaster recovery

---

# 50 Linux Troubleshooting Interview Questions

## Beginner

1. What is Linux troubleshooting?
2. What is system load?
3. What is OOM kill?
4. What is systemctl?
5. What is journalctl?
6. What is dmesg?
7. What is inode exhaustion?
8. What is swap memory?
9. What is DNS resolution?
10. What is TCP connection?

---

## Intermediate

11. Difference between CPU and load average?
12. Explain Linux boot process.
13. What causes high memory usage?
14. Explain disk I/O bottleneck.
15. Difference between TCP and UDP?
16. Explain systemd.
17. What is zombie process?
18. Explain process states.
19. What is packet capture?
20. Explain DNS troubleshooting.

---

## Advanced

21. Explain Linux kernel internals.
22. What is context switching?
23. Explain cgroups.
24. What is namespace isolation?
25. Explain TCP three-way handshake.
26. What is SYN flood?
27. Explain Linux scheduler.
28. What is inode exhaustion?
29. Explain memory fragmentation.
30. What is kernel panic?

---

## Production Based

31. Server extremely slow investigation.
32. Kubernetes pod crash debugging.
33. Docker container failure investigation.
34. High disk usage troubleshooting.
35. DNS outage debugging.
36. Memory leak investigation.
37. Network latency investigation.
38. Production incident handling.
39. Root cause analysis workflow.
40. Service outage troubleshooting.

---

## Scenario Based

41. Entire application inaccessible.
42. Kubernetes nodes NotReady.
43. Docker daemon stopped unexpectedly.
44. CPU suddenly reaches 100%.
45. Database server disk full.
46. Logs consuming all storage.
47. DNS resolution failing.
48. SSH access lost.
49. Kubernetes pods restarting continuously.
50. Explain your production debugging workflow.

---

# Summary

Linux troubleshooting is one of the most critical real-world DevOps skills.

Strong troubleshooting skills are essential for:
- incident response
- production debugging
- infrastructure reliability
- Kubernetes operations
- cloud engineering

Senior DevOps engineers spend significant time:
- debugging systems
- investigating outages
- analyzing logs
- fixing infrastructure
- improving reliability
