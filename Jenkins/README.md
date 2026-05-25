# Jenkins for DevOps Engineers

# Introduction

Jenkins is an open-source automation server used for:
- CI/CD pipelines
- automated testing
- deployments
- infrastructure automation
- DevOps workflows

Jenkins integrates with:
- GitHub
- Docker
- Kubernetes
- Terraform
- SonarQube
- AWS
- Ansible

---

# What is CI/CD?

# Continuous Integration (CI)

Developers frequently merge code changes.

CI automates:
- build
- testing
- validation

---

# Continuous Delivery (CD)

CD automates:
- deployment
- release workflows

---

# Jenkins Architecture

Jenkins consists of:

| Component | Purpose |
|---|---|
| Jenkins Master | manages pipelines |
| Jenkins Agent | executes jobs |
| Plugins | extend Jenkins features |
| Pipeline | CI/CD workflow |

---

# Jenkins Workflow

1. Developer pushes code
2. GitHub webhook triggers Jenkins
3. Jenkins pulls code
4. Build starts
5. Tests run
6. Docker image built
7. Image pushed
8. Deployment triggered

---

# Install Java

Purpose:
- Jenkins requires Java runtime

Command:

```bash
sudo apt update
sudo apt install openjdk-17-jdk -y
```

---

# Verify Java

Purpose:
- checks Java installation

Command:

```bash
java -version
```

---

# Install Jenkins

Purpose:
- installs Jenkins server

Commands:

```bash
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
```

```bash
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
```

```bash
sudo apt update
sudo apt install jenkins -y
```

---

# Start Jenkins

Purpose:
- starts Jenkins service

Command:

```bash
sudo systemctl start jenkins
```

---

# Enable Jenkins

Purpose:
- auto-start Jenkins after reboot

Command:

```bash
sudo systemctl enable jenkins
```

---

# Check Jenkins Status

Purpose:
- verifies Jenkins service health

Command:

```bash
sudo systemctl status jenkins
```

---

# Access Jenkins Initial Password

Purpose:
- retrieves admin unlock password

Command:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

---

# Jenkins Dashboard

Default Port:
- 8080

Access:

```text
http://SERVER-IP:8080
```

---

# Jenkins Jobs

A job is a task executed by Jenkins.

Types:
- Freestyle
- Pipeline
- Multibranch Pipeline

---

# Freestyle Job

Simple GUI-based automation job.

Used for:
- beginners
- simple builds

---

# Jenkins Pipeline

Pipeline defines CI/CD workflow as code.

Advantages:
- version controlled
- reusable
- scalable

---

# Declarative Pipeline

Purpose:
- structured pipeline syntax

Example:

```groovy
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building Application'
            }
        }
    }
}
```

---

# Scripted Pipeline

Purpose:
- advanced flexible pipeline scripting

Example:

```groovy
node {
    stage('Build') {
        echo 'Building'
    }
}
```

---

# Create Jenkinsfile

Purpose:
- stores pipeline as code

Command:

```bash
vim Jenkinsfile
```

Example:

```groovy
pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                git 'https://github.com/user/repo.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t app .'
            }
        }
    }
}
```

---

# Jenkins Agents

Agents execute jobs.

Types:
- static agents
- dynamic agents
- Kubernetes agents

---

# Jenkins Plugins

Plugins extend Jenkins functionality.

Popular Plugins:
- Git
- Docker
- Kubernetes
- Pipeline
- Blue Ocean
- SonarQube

---

# Install Plugins

Purpose:
- adds Jenkins features

Location:
- Manage Jenkins → Plugins

---

# Jenkins Credentials

Stores:
- passwords
- API keys
- SSH keys
- tokens

---

# Add Credentials

Location:
- Manage Jenkins → Credentials

---

# GitHub Webhooks

Purpose:
- automatically trigger pipelines

Webhook URL:

```text
http://JENKINS-IP:8080/github-webhook/
```

---

# Docker Integration

Jenkins can:
- build Docker images
- push images
- deploy containers

---

# Kubernetes Integration

Jenkins can:
- deploy to Kubernetes
- create dynamic agents
- manage Helm deployments

---

# Jenkins Shared Libraries

Purpose:
- reusable pipeline code

Benefits:
- standardization
- maintainability

---

# Backup Jenkins

Purpose:
- protects Jenkins configurations

Important Directories:

```bash
/var/lib/jenkins
```

Backup Command:

```bash
tar -czvf jenkins-backup.tar.gz /var/lib/jenkins
```

---

# Restore Jenkins

Purpose:
- restores Jenkins data

Command:

```bash
tar -xzvf jenkins-backup.tar.gz
```

---

# Jenkins Logs

Purpose:
- investigates failures

Command:

```bash
sudo journalctl -u jenkins
```

---

# Restart Jenkins

Purpose:
- applies changes

Command:

```bash
sudo systemctl restart jenkins
```

---

# Jenkins Security Best Practices

- use RBAC
- enable HTTPS
- restrict plugins
- secure credentials
- backup Jenkins
- use agents
- avoid running builds on master

---

# Jenkins Pipeline Stages

Common Stages:
- Checkout
- Build
- Test
- Security Scan
- Docker Build
- Push Image
- Deploy

---

# CI/CD Production Workflow

1. Developer pushes code
2. GitHub webhook triggers Jenkins
3. Jenkins builds application
4. SonarQube scans code
5. Docker image built
6. Image pushed to registry
7. Kubernetes deployment updated

---

# Jenkins Troubleshooting

# Check Jenkins Service

Purpose:
- verifies Jenkins health

Command:

```bash
systemctl status jenkins
```

---

# Check Logs

Purpose:
- investigates pipeline failures

Command:

```bash
journalctl -u jenkins
```

---

# Check Disk Usage

Purpose:
- Jenkins failures often caused by disk full

Command:

```bash
df -h
```

---

# Check Port Usage

Purpose:
- verifies Jenkins port availability

Command:

```bash
ss -tulpn | grep 8080
```

---

# Restart Jenkins

Purpose:
- resolves temporary issues

Command:

```bash
systemctl restart jenkins
```

---

# 50 Most Used Jenkins Commands

| Command | Purpose |
|---|---|
| systemctl start jenkins | start Jenkins |
| systemctl stop jenkins | stop Jenkins |
| systemctl restart jenkins | restart Jenkins |
| systemctl status jenkins | Jenkins status |
| journalctl -u jenkins | Jenkins logs |
| java -version | check Java |
| mvn clean package | Maven build |
| gradle build | Gradle build |
| docker build | build image |
| docker push | push image |
| kubectl apply -f | deploy Kubernetes |
| helm install | install Helm chart |
| git clone | clone repository |
| git pull | pull changes |
| ansible-playbook | run automation |
| terraform init | initialize Terraform |
| terraform apply | apply infrastructure |
| sonar-scanner | run SonarQube scan |
| trivy image | container scan |
| npm install | install dependencies |
| npm test | run tests |
| pytest | Python tests |
| chmod +x | make executable |
| curl | API requests |
| wget | download files |
| tar -czvf | create backup |
| unzip | extract files |
| ssh | remote access |
| scp | transfer files |
| rsync | synchronize data |
| ps -ef | running processes |
| top | system usage |
| free -h | memory usage |
| uptime | server uptime |
| kubectl get pods | Kubernetes pods |
| docker ps | running containers |
| docker logs | container logs |
| docker exec | container shell |
| kubectl logs | pod logs |
| kubectl describe | resource details |
| aws s3 ls | list S3 buckets |
| aws ec2 describe-instances | EC2 details |
| netstat -tulpn | listening ports |
| ss -tulpn | socket statistics |
| crontab -e | edit cron jobs |
| env | environment variables |
| export | export variables |
| source | reload shell |
| vim Jenkinsfile | edit pipeline |
| cat | view files |

---

# Real World Production Scenarios

# Scenario 1 — Jenkins Pipeline Failing

Symptoms:
- build failed

Investigation:

```bash
journalctl -u jenkins
```

Possible Causes:
- syntax issue
- missing dependency
- agent unavailable

---

# Scenario 2 — Jenkins Server Disk Full

Symptoms:
- builds fail suddenly

Investigation:

```bash
df -h
```

Cleanup:
- remove old builds
- clean Docker images

---

# Scenario 3 — GitHub Webhook Not Triggering

Investigation:
- webhook configuration
- Jenkins URL
- firewall rules

---

# Scenario 4 — Docker Build Failure

Investigation:

```bash
docker logs CONTAINER_ID
```

Possible Causes:
- Dockerfile syntax issue
- dependency failure

---

# Scenario 5 — Jenkins Agent Offline

Investigation:
- SSH connectivity
- Java availability
- network issue

---

# Production Troubleshooting Workflow

# Step 1 — Check Jenkins Status

```bash
systemctl status jenkins
```

---

# Step 2 — Check Logs

```bash
journalctl -u jenkins
```

---

# Step 3 — Verify Disk Usage

```bash
df -h
```

---

# Step 4 — Verify Java

```bash
java -version
```

---

# Step 5 — Verify Port

```bash
ss -tulpn | grep 8080
```

---

# Step 6 — Verify Plugins

Location:
- Manage Jenkins → Plugins

---

# Jenkins Best Practices

- pipeline as code
- use agents
- backup Jenkins
- secure credentials
- automate cleanup
- avoid freestyle jobs
- use shared libraries
- monitor Jenkins health

---

# Jenkins Scaling Strategies

- distributed builds
- Kubernetes agents
- shared libraries
- cloud agents
- load balancing

---

# 50 Jenkins Interview Questions

## Beginner

1. What is Jenkins?
2. What is CI/CD?
3. What is pipeline?
4. Difference between freestyle and pipeline job?
5. What is Jenkinsfile?
6. What are Jenkins agents?
7. What are plugins?
8. What is webhook?
9. What is declarative pipeline?
10. What is scripted pipeline?

---

## Intermediate

11. Difference between CI and CD?
12. Explain Jenkins architecture.
13. What are shared libraries?
14. What is Blue Ocean?
15. Explain Jenkins agents.
16. How Jenkins integrates with Docker?
17. How Jenkins integrates with Kubernetes?
18. What is multibranch pipeline?
19. Explain Jenkins credentials.
20. What is build trigger?

---

## Advanced

21. Explain Jenkins master-agent communication.
22. How to secure Jenkins?
23. Explain Jenkins scalability.
24. How Jenkins handles parallel builds?
25. Explain Jenkins shared library architecture.
26. What are pipeline stages?
27. Explain Jenkins backup strategy.
28. What is Jenkins CPS?
29. Explain Jenkins plugin architecture.
30. How to optimize Jenkins performance?

---

## Production Based

31. Jenkins server disk full troubleshooting.
32. Pipeline suddenly failing.
33. Jenkins agent offline debugging.
34. GitHub webhook issue investigation.
35. Docker build failure in Jenkins.
36. Kubernetes deployment failure from Jenkins.
37. Jenkins plugin conflict handling.
38. Secure credentials management.
39. Jenkins backup and disaster recovery.
40. Jenkins scaling strategy.

---

## Scenario Based

41. Jenkins UI inaccessible.
42. Pipeline stuck in running state.
43. Jenkins build queue extremely high.
44. Jenkins job triggered multiple times.
45. Jenkins upgrade failed.
46. Pipeline cannot access Docker daemon.
47. Jenkins unable to clone repository.
48. Shared library breaking pipelines.
49. Jenkins consuming high memory.
50. Explain your end-to-end CI/CD workflow using Jenkins.

---

# Summary

Jenkins is one of the most important CI/CD tools in DevOps.

Strong Jenkins skills are essential for:
- automation
- CI/CD pipelines
- deployments
- infrastructure orchestration
- enterprise DevOps workflows

Senior DevOps engineers spend significant time:
- building pipelines
- debugging failures
- integrating tools
- automating deployments
- optimizing CI/CD infrastructure
