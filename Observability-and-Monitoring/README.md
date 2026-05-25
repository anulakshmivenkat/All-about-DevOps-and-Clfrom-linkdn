# Prometheus and Grafana for DevOps Engineers

# Introduction

Prometheus is an open-source monitoring and alerting tool.

Grafana is a visualization and dashboard platform.

Together they provide:
- infrastructure monitoring
- Kubernetes monitoring
- container monitoring
- application monitoring
- alerting
- observability

---

# Why Monitoring Matters

Without monitoring:
- production failures remain unnoticed
- debugging becomes difficult
- downtime increases
- performance issues go undetected

Monitoring helps:
- detect failures early
- investigate incidents
- optimize performance
- improve reliability

---

# Prometheus Architecture

Prometheus consists of:

| Component | Purpose |
|---|---|
| Prometheus Server | collects metrics |
| Exporter | exposes metrics |
| TSDB | stores metrics |
| Alertmanager | handles alerts |
| PromQL | query language |

---

# Grafana Architecture

Grafana consists of:

| Component | Purpose |
|---|---|
| Dashboard | visualization |
| Data Source | metric provider |
| Panel | visualization widget |
| Alerting | notifications |

---

# Common Exporters

| Exporter | Purpose |
|---|---|
| Node Exporter | Linux server metrics |
| kube-state-metrics | Kubernetes metrics |
| cAdvisor | container metrics |
| Blackbox Exporter | endpoint monitoring |

---

# Install Prometheus

# Create User

Purpose:
- creates dedicated Prometheus user

Command:

```bash
sudo useradd --no-create-home --shell /bin/false prometheus
```

---

# Download Prometheus

Purpose:
- downloads Prometheus binaries

Command:

```bash
wget https://github.com/prometheus/prometheus/releases/download/v2.52.0/prometheus-2.52.0.linux-amd64.tar.gz
```

---

# Extract Files

Purpose:
- extracts Prometheus archive

Command:

```bash
tar -xvf prometheus-2.52.0.linux-amd64.tar.gz
```

---

# Move Files

Purpose:
- organizes installation

Command:

```bash
sudo mv prometheus-2.52.0.linux-amd64 /etc/prometheus
```

---

# Verify Prometheus

Purpose:
- checks Prometheus version

Command:

```bash
/etc/prometheus/prometheus --version
```

---

# Install Node Exporter

Purpose:
- exposes Linux server metrics

Command:

```bash
wget https://github.com/prometheus/node_exporter/releases/download/v1.8.1/node_exporter-1.8.1.linux-amd64.tar.gz
```

---

# Extract Node Exporter

Purpose:
- extracts exporter binaries

Command:

```bash
tar -xvf node_exporter-1.8.1.linux-amd64.tar.gz
```

---

# Start Node Exporter

Purpose:
- starts metrics exporter

Command:

```bash
./node_exporter
```

---

# Prometheus Configuration

Configuration File:

```bash
prometheus.yml
```

---

# Edit Prometheus Configuration

Purpose:
- defines scrape targets

Command:

```bash
vim prometheus.yml
```

Example:

```yaml
scrape_configs:
  - job_name: "node"

    static_configs:
      - targets: ["localhost:9100"]
```

---

# Start Prometheus

Purpose:
- starts Prometheus server

Command:

```bash
./prometheus --config.file=prometheus.yml
```

---

# Prometheus UI

Default Port:
- 9090

Access:

```text
http://SERVER-IP:9090
```

---

# Install Grafana

# Add Grafana Repository

Purpose:
- adds Grafana package source

Command:

```bash
sudo apt-get install -y software-properties-common
```

---

# Install Grafana

Purpose:
- installs Grafana dashboard platform

Command:

```bash
sudo apt install grafana -y
```

---

# Start Grafana

Purpose:
- starts Grafana service

Command:

```bash
sudo systemctl start grafana-server
```

---

# Enable Grafana

Purpose:
- auto-starts Grafana after reboot

Command:

```bash
sudo systemctl enable grafana-server
```

---

# Check Grafana Status

Purpose:
- verifies Grafana health

Command:

```bash
sudo systemctl status grafana-server
```

---

# Grafana UI

Default Port:
- 3000

Access:

```text
http://SERVER-IP:3000
```

Default Credentials:

```text
admin/admin
```

---

# Add Prometheus Data Source

Location:
- Grafana → Connections → Data Sources

Prometheus URL:

```text
http://localhost:9090
```

---

# PromQL

PromQL is Prometheus query language.

---

# CPU Usage Query

Purpose:
- monitors CPU usage

Example:

```promql
100 - (avg by(instance)(rate(node_cpu_seconds_total{mode="idle"}[5m])) * 100)
```

---

# Memory Usage Query

Purpose:
- monitors memory utilization

Example:

```promql
(node_memory_MemTotal_bytes - node_memory_MemAvailable_bytes)
```

---

# Disk Usage Query

Purpose:
- monitors storage utilization

Example:

```promql
node_filesystem_avail_bytes
```

---

# Kubernetes Monitoring

Prometheus commonly monitors:
- pods
- nodes
- deployments
- API server
- etcd

---

# Alertmanager

Alertmanager handles:
- alerts
- notifications
- grouping
- silencing

---

# Alert Rule Example

```yaml
groups:
  - name: node-alerts

    rules:
      - alert: HighCPUUsage
        expr: cpu_usage > 80
```

---

# Monitoring Best Practices

- monitor infrastructure
- monitor applications
- implement alerting
- use dashboards
- avoid alert fatigue
- define SLOs

---

# Prometheus Troubleshooting

# Check Prometheus Status

Purpose:
- verifies service health

Command:

```bash
systemctl status prometheus
```

---

# Verify Scrape Targets

Purpose:
- checks monitored targets

Location:
- Prometheus UI → Targets

---

# Check Prometheus Logs

Purpose:
- debug monitoring failures

Command:

```bash
journalctl -u prometheus
```

---

# Verify Exporter Metrics

Purpose:
- checks exporter output

Command:

```bash
curl localhost:9100/metrics
```

---

# Verify Port Usage

Purpose:
- checks listening services

Command:

```bash
ss -tulpn
```

---

# Grafana Troubleshooting

# Check Grafana Status

Purpose:
- verifies Grafana service

Command:

```bash
systemctl status grafana-server
```

---

# Check Grafana Logs

Purpose:
- investigates dashboard issues

Command:

```bash
journalctl -u grafana-server
```

---

# Verify Data Source

Purpose:
- confirms Prometheus connectivity

Location:
- Grafana → Data Sources

---

# 50 Most Used Prometheus and Grafana Commands

| Command | Purpose |
|---|---|
| systemctl start prometheus | start Prometheus |
| systemctl stop prometheus | stop Prometheus |
| systemctl restart prometheus | restart Prometheus |
| systemctl status prometheus | Prometheus status |
| journalctl -u prometheus | Prometheus logs |
| curl localhost:9100/metrics | exporter metrics |
| wget | download binaries |
| tar -xvf | extract archives |
| ss -tulpn | listening ports |
| netstat -tulpn | port details |
| systemctl start grafana-server | start Grafana |
| systemctl stop grafana-server | stop Grafana |
| systemctl restart grafana-server | restart Grafana |
| systemctl status grafana-server | Grafana status |
| journalctl -u grafana-server | Grafana logs |
| kubectl get pods | Kubernetes monitoring |
| kubectl top nodes | node metrics |
| kubectl top pods | pod metrics |
| helm install | install monitoring stack |
| helm upgrade | upgrade charts |
| docker ps | running containers |
| docker logs | container logs |
| docker stats | container metrics |
| free -h | memory usage |
| top | system usage |
| htop | interactive monitoring |
| df -h | disk usage |
| iostat | disk performance |
| vmstat | system performance |
| sar | system activity |
| uptime | load average |
| ps -ef | running processes |
| cat /proc/cpuinfo | CPU details |
| cat /proc/meminfo | memory info |
| curl | API checks |
| vim prometheus.yml | edit config |
| cat | view config |
| grep | search logs |
| awk | process logs |
| sed | edit streams |
| chmod +x | executable permission |
| ping | connectivity |
| traceroute | network path |
| dig | DNS lookup |
| nslookup | DNS query |
| kubectl describe pod | pod details |
| kubectl logs | pod logs |
| docker exec | container shell |
| terraform apply | infrastructure deployment |
| ansible-playbook | automation |

---

# Real World Production Scenarios

# Scenario 1 — Prometheus Not Scraping Targets

Symptoms:
- no metrics available

Investigation:
- verify target configuration
- verify firewall
- verify exporter

Check:

```bash
curl localhost:9100/metrics
```

---

# Scenario 2 — High Memory Usage

Symptoms:
- Prometheus consuming excessive RAM

Possible Causes:
- high metric cardinality
- too many scrape targets

Fix:
- reduce retention
- optimize metrics

---

# Scenario 3 — Grafana Dashboard Empty

Investigation:
- data source issue
- Prometheus unreachable
- incorrect query

Fix:
- verify Prometheus URL
- validate PromQL query

---

# Scenario 4 — Kubernetes Metrics Missing

Investigation:
- metrics-server issue
- RBAC issue
- exporter failure

Check:

```bash
kubectl get pods -A
```

---

# Scenario 5 — Alert Not Triggering

Investigation:
- incorrect PromQL
- Alertmanager issue
- alert rule syntax error

---

# Production Troubleshooting Workflow

# Step 1 — Verify Prometheus Service

```bash
systemctl status prometheus
```

---

# Step 2 — Verify Exporters

```bash
curl localhost:9100/metrics
```

---

# Step 3 — Verify Targets

Location:
- Prometheus UI → Targets

---

# Step 4 — Verify Grafana

```bash
systemctl status grafana-server
```

---

# Step 5 — Verify Queries

Test PromQL inside Prometheus UI.

---

# Step 6 — Verify Infrastructure

```bash
kubectl top nodes
```

---

# Enterprise Monitoring Workflow

1. Exporters expose metrics
2. Prometheus scrapes metrics
3. Metrics stored in TSDB
4. Grafana visualizes metrics
5. Alertmanager sends alerts
6. Engineers investigate incidents

---

# Prometheus and Grafana Best Practices

- implement alerting
- monitor infrastructure
- avoid excessive metrics
- secure dashboards
- define retention policies
- use labels carefully
- implement HA monitoring

---

# 50 Prometheus and Grafana Interview Questions

## Beginner

1. What is Prometheus?
2. What is Grafana?
3. What is monitoring?
4. What is exporter?
5. What is PromQL?
6. What is Alertmanager?
7. What is time series data?
8. What is scrape target?
9. What is dashboard?
10. What is metrics collection?

---

## Intermediate

11. Explain Prometheus architecture.
12. Explain Grafana architecture.
13. Difference between monitoring and observability?
14. What is node exporter?
15. Explain Prometheus pull model.
16. What is retention policy?
17. Explain Grafana data source.
18. What is alert rule?
19. What is label in Prometheus?
20. Explain Kubernetes monitoring.

---

## Advanced

21. Explain Prometheus TSDB internals.
22. What is high cardinality?
23. Explain Alertmanager routing.
24. What is federation in Prometheus?
25. Explain recording rules.
26. What is remote write?
27. Explain service discovery.
28. What is histogram metric?
29. Explain PromQL optimization.
30. What is HA monitoring setup?

---

## Production Based

31. Prometheus high memory troubleshooting.
32. Grafana dashboard not loading.
33. Exporter metrics missing.
34. Alertmanager not sending alerts.
35. Kubernetes monitoring issue investigation.
36. Monitoring large scale infrastructure.
37. Prometheus storage optimization.
38. Monitoring security best practices.
39. Production incident investigation workflow.
40. Alert fatigue reduction strategy.

---

## Scenario Based

41. Entire monitoring stack down.
42. Metrics suddenly disappeared.
43. Grafana showing no data.
44. Prometheus disk full.
45. Alert storm in production.
46. Node exporter unreachable.
47. Kubernetes metrics partially missing.
48. PromQL query extremely slow.
49. Monitoring consuming high resources.
50. Explain your production monitoring architecture.

---

# Summary

Prometheus and Grafana are critical tools in DevOps and SRE.

Strong monitoring skills are essential for:
- infrastructure reliability
- incident investigation
- observability
- Kubernetes operations
- production debugging

Senior DevOps engineers spend significant time:
- monitoring systems
- debugging incidents
- analyzing metrics
- building dashboards
- improving reliability
