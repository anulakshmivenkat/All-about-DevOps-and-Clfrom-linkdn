# Django for DevOps Engineers

# Introduction

Django is a powerful Python web framework used for:
- enterprise applications
- admin dashboards
- cloud platforms
- automation systems
- internal tools

Django provides:
- authentication
- ORM
- admin panel
- scalability
- security

---

# Install Django

Purpose:
- install framework

Command:

```bash
pip3 install django
```

---

# Verify Django

Purpose:
- verify installation

Command:

```bash
django-admin --version
```

---

# Create Django Project

Purpose:
- initialize project

Command:

```bash
django-admin startproject devopsproject
```

---

# Navigate Project

Command:

```bash
cd devopsproject
```

---

# Run Django Server

Purpose:
- start development server

Command:

```bash
python3 manage.py runserver 0.0.0.0:8000
```

---

# Access Django Application

URL:

```text
http://SERVER-IP:8000
```

---

# Django Project Structure

```text
devopsproject/
├── manage.py
├── devopsproject/
│   ├── settings.py
│   ├── urls.py
│   ├── wsgi.py
```

---

# Create Django App

Purpose:
- modular application

Command:

```bash
python3 manage.py startapp monitoring
```

---

# Django Models

Purpose:
- database tables

Example:

```python
from django.db import models

class Server(models.Model):
    name = models.CharField(max_length=100)
    status = models.CharField(max_length=50)
```

---

# Apply Database Migration

Purpose:
- create tables

Commands:

```bash
python3 manage.py makemigrations
```

```bash
python3 manage.py migrate
```

---

# Create Admin User

Purpose:
- Django admin panel

Command:

```bash
python3 manage.py createsuperuser
```

---

# Django Admin Panel

URL:

```text
http://SERVER-IP:8000/admin
```

---

# Install Django REST Framework

Purpose:
- API development

Command:

```bash
pip3 install djangorestframework
```

---

# Django REST API Example

Example:

```python
from rest_framework.views import APIView
from rest_framework.response import Response

class Health(APIView):

    def get(self, request):
        return Response({"status":"healthy"})
```

---

# Django Static Files

Purpose:
- CSS/JS/images

Command:

```bash
python3 manage.py collectstatic
```

---

# Django Environment Variables

Purpose:
- secure configuration

Example:

```bash
export SECRET_KEY=mysecret
```

---

# Django with PostgreSQL

Install PostgreSQL Driver:

```bash
pip3 install psycopg2-binary
```

---

# Django Production Deployment

Architecture:

NGINX → Gunicorn → Django → PostgreSQL

---

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
gunicorn devopsproject.wsgi:application
```

---

# Dockerize Django Application

# Create Dockerfile

Command:

```bash
vim Dockerfile
```

---

# Django Dockerfile

Example:

```dockerfile
FROM python:3.11

WORKDIR /app

COPY . .

RUN pip install -r requirements.txt

CMD ["gunicorn", "devopsproject.wsgi:application", "--bind", "0.0.0.0:8000"]
```

---

# Build Docker Image

Purpose:
- create container image

Command:

```bash
docker build -t django-devops .
```

---

# Run Docker Container

Purpose:
- run application

Command:

```bash
docker run -d -p 8000:8000 django-devops
```

---

# Kubernetes Deployment

# deployment.yaml

Example:

```yaml
apiVersion: apps/v1
kind: Deployment

metadata:
  name: django-app

spec:
  replicas: 2

  selector:
    matchLabels:
      app: django

  template:
    metadata:
      labels:
        app: django

    spec:
      containers:
      - name: django
        image: username/django-devops
        ports:
        - containerPort: 8000
```

---

# Deploy Django App

Purpose:
- Kubernetes deployment

Command:

```bash
kubectl apply -f deployment.yaml
```

---

# Expose Django Service

Purpose:
- access application

Command:

```bash
kubectl expose deployment django-app \
--type=NodePort \
--port=8000
```

---

# Django Real World DevOps Use Cases

| Use Case | Purpose |
|---|---|
| Internal DevOps Portal | infrastructure management |
| Monitoring Platform | observability |
| Cloud Dashboard | cloud operations |
| Automation Platform | self-service infrastructure |
| Incident Dashboard | operations management |

---

# Django Troubleshooting

# Migration Failure

Check:

```bash
python3 manage.py showmigrations
```

---

# Gunicorn Failure

Check:

```bash
journalctl -u gunicorn
```

---

# Static Files Not Loading

Run:

```bash
python3 manage.py collectstatic
```

---

# Kubernetes Deployment Failure

Check:

```bash
kubectl logs POD_NAME
kubectl describe pod POD_NAME
```

---

# Django Interview Questions with Answers

# 1. What is Django?

Answer:

Django is a high-level Python web framework used for scalable web applications.

---

# 2. Why use Django in DevOps?

Answer:

Django is used for:
- internal portals
- automation platforms
- dashboards
- APIs

---

# 3. What is Gunicorn?

Answer:

Gunicorn is a Python WSGI HTTP server used for production deployment.

---

# 4. Why use PostgreSQL with Django?

Answer:

PostgreSQL provides:
- reliability
- scalability
- enterprise-grade database features

---

# 5. How do you deploy Django in Kubernetes?

Answer:

Steps:
- containerize app
- push Docker image
- create Kubernetes manifests
- expose application

---

# Summary

Django is heavily used in enterprise DevOps environments for:
- dashboards
- automation systems
- cloud platforms
- infrastructure management tools
