# Flask for DevOps Engineers

# Introduction

Flask is a lightweight Python web framework.

DevOps engineers use Flask for:
- automation APIs
- internal dashboards
- monitoring systems
- health check APIs
- webhook receivers
- CI/CD integrations

Flask is simple, lightweight, and easy to containerize.

---

# Install Flask

Purpose:
- install Flask framework

Command:

```bash
pip3 install flask
```

---

# Verify Flask

Purpose:
- verify installation

Command:

```bash
pip3 list | grep Flask
```

---

# Create Flask Application

Purpose:
- create application file

Command:

```bash
vim app.py
```

---

# Basic Flask App

Example:

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def home():
    return "DevOps Flask Application"

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

---

# Run Flask Application

Purpose:
- start server

Command:

```bash
python3 app.py
```

---

# Access Application

Purpose:
- verify application

URL:

```text
http://SERVER-IP:5000
```

---

# Flask API Example

Purpose:
- build automation API

Example:

```python
from flask import Flask, jsonify

app = Flask(__name__)

@app.route("/health")
def health():
    return jsonify({"status": "healthy"})
```

---

# Install Virtual Environment

Purpose:
- isolate dependencies

Command:

```bash
python3 -m venv venv
```

---

# Activate Virtual Environment

Purpose:
- activate environment

Command:

```bash
source venv/bin/activate
```

---

# requirements.txt

Purpose:
- dependency management

Command:

```bash
pip3 freeze > requirements.txt
```

---

# Install Dependencies

Purpose:
- install packages

Command:

```bash
pip3 install -r requirements.txt
```

---

# Flask Environment Variables

Purpose:
- runtime configuration

Example:

```bash
export FLASK_APP=app.py
export FLASK_ENV=development
```

---

# Run Flask Using Flask CLI

Purpose:
- start application

Command:

```bash
flask run --host=0.0.0.0
```

---

# Flask Logging

Purpose:
- application logs

Example:

```python
import logging

logging.basicConfig(level=logging.INFO)

logging.info("Flask App Started")
```

---

# Flask Health Check API

Purpose:
- Kubernetes readiness/liveness probe

Example:

```python
@app.route("/health")
def health():
    return "OK", 200
```

---

# Dockerize Flask Application

# Create Dockerfile

Purpose:
- containerize application

Command:

```bash
vim Dockerfile
```

---

# Flask Dockerfile

Example:

```dockerfile
FROM python:3.11

WORKDIR /app

COPY . .

RUN pip install -r requirements.txt

CMD ["python3", "app.py"]
```

---

# Build Docker Image

Purpose:
- create image

Command:

```bash
docker build -t flask-devops .
```

---

# Run Docker Container

Purpose:
- run application

Command:

```bash
docker run -d -p 5000:5000 flask-devops
```

---

# Push Image to DockerHub

Purpose:
- upload image

Command:

```bash
docker tag flask-devops username/flask-devops
```

```bash
docker push username/flask-devops
```

---

# Flask Kubernetes Deployment

# deployment.yaml

Example:

```yaml
apiVersion: apps/v1
kind: Deployment

metadata:
  name: flask-app

spec:
  replicas: 2

  selector:
    matchLabels:
      app: flask

  template:
    metadata:
      labels:
        app: flask

    spec:
      containers:
      - name: flask
        image: username/flask-devops
        ports:
        - containerPort: 5000
```

---

# Deploy Flask App

Purpose:
- deploy to Kubernetes

Command:

```bash
kubectl apply -f deployment.yaml
```

---

# Expose Flask Application

Purpose:
- access application

Command:

```bash
kubectl expose deployment flask-app \
--type=NodePort \
--port=5000
```

---

# Flask with Gunicorn

# Install Gunicorn

Purpose:
- production WSGI server

Command:

```bash
pip3 install gunicorn
```

---

# Run Gunicorn

Purpose:
- production deployment

Command:

```bash
gunicorn -w 4 -b 0.0.0.0:5000 app:app
```

---

# Flask with NGINX

Purpose:
- reverse proxy

Architecture:

NGINX → Gunicorn → Flask

---

# Flask Real World DevOps Use Cases

| Use Case | Purpose |
|---|---|
| Monitoring dashboard | infrastructure visibility |
| Webhook API | CI/CD integration |
| Health check API | Kubernetes probes |
| Automation portal | infrastructure operations |
| Alert receiver | incident handling |

---

# Flask Troubleshooting

# Flask App Not Starting

Check:

```bash
python3 app.py
```

---

# Port Already in Use

Investigation:

```bash
ss -tulpn | grep 5000
```

---

# Docker Container Crashing

Check:

```bash
docker logs CONTAINER_ID
```

---

# Kubernetes Pod Failure

Check:

```bash
kubectl describe pod POD_NAME
kubectl logs POD_NAME
```

---

# Flask Interview Questions with Answers

# 1. What is Flask?

Answer:

Flask is a lightweight Python web framework used for APIs and web applications.

---

# 2. Why is Flask used in DevOps?

Answer:

Flask is used for:
- automation APIs
- dashboards
- health checks
- integrations

---

# 3. What is Gunicorn?

Answer:

Gunicorn is a production-grade Python WSGI server.

---

# 4. Why use NGINX with Flask?

Answer:

NGINX provides:
- reverse proxy
- load balancing
- SSL termination

---

# 5. How do you deploy Flask in Kubernetes?

Answer:

Steps:
- containerize app
- push Docker image
- create deployment YAML
- expose service

---

# Summary

Flask is widely used in DevOps for:
- APIs
- dashboards
- automation
- cloud-native tooling
- Kubernetes integrations
