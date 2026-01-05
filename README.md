# Healthcare Prediction API – DevOps Assignment

## Overview
This project demonstrates a production-ready DevOps workflow for a healthcare-style microservice.
It covers containerization, CI/CD automation, Kubernetes deployment design, monitoring strategy,
and security best practices.

The application exposes two REST endpoints:
- `GET /health` – service health check
- `GET /predict` – returns a sample prediction score `{ "score": 0.75 }`

---

## Architecture Overview

**High-Level Flow:**

Developer → GitHub  
→ CI/CD Pipeline (Jenkins)  
→ Docker Hub  
→ Kubernetes Cluster (EKS / Local)  
→ Monitoring & Alerts

---

## 1. Application & Containerization

### Technology Stack
- Language: Python (FastAPI)
- Containerization: Docker
- CI/CD Tool: Jenkins
- Orchestration: Kubernetes (design + manifests)

### Docker Implementation
- Multi-stage Dockerfile
- Non-root container execution
- Lightweight base image
- Health check endpoint exposed

Docker image is built and pushed to Docker Hub via Jenkins pipeline.

---

## 2. CI/CD Pipeline (Jenkins)

### Continuous Integration (CI)
- Source code checkout from GitHub
- Application build and validation
- Docker image build
- Docker image push to Docker Hub

### Continuous Deployment (CD)
- Kubernetes deployment manifests prepared
- Rolling update strategy configured
- Designed for EKS / KIND / Docker Desktop Kubernetes

Pipeline automation ensures repeatable and reliable deployments.

---

## 3. Kubernetes Deployment

### Kubernetes Resources
- Deployment (replicas, rolling updates)
- Service (ClusterIP / NodePort)
- Liveness and readiness probes
- Resource requests and limits

### Deployment Status
Due to Docker Desktop Kubernetes cluster initialization issues on the local system,
live cluster deployment could not be completed within the assignment timeline.

However:
- Kubernetes manifests are production-ready
- Compatible with AWS EKS and KIND clusters
- Health probes and rolling update strategy are fully configured

---

## 4. Monitoring & Alerts (Design)

### Metrics Considered
- CPU utilization
- Memory utilization
- Pod restart count
- Health check failures

### Dashboard Design
Monitoring is designed using:
- AWS CloudWatch Container Insights (for EKS)
- OR Grafana dashboards (Prometheus-based)

### Alert Strategy

| Alert Type | Threshold |
|-----------|----------|
| High CPU Usage | > 70% for 5 minutes |
| High Memory Usage | > 80% |
| Health Check Failure | Liveness probe failure |

---

## 5. Security Best Practices

- Least-privilege IAM roles (CI/CD and Kubernetes)
- No credentials stored in GitHub repository
- Secrets managed via AWS Secrets Manager / SSM (design)
- HTTPS enforced using Load Balancer / Ingress (production design)
- Container runs as a non-root user

---

## 6. Repository Structure

```text
.
├── app/
│   └── main.py
├── Dockerfile
├── requirements.txt
├── kubernetes_deployment/
│   ├── deployment.yaml
│   └── service.yaml
├── Jenkinsfile
└── README.md
