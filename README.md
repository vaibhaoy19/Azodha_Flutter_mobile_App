# Healthcare Prediction API – DevOps Assignment

## Overview
This project demonstrates a production-ready DevOps workflow for a healthcare-style microservice.
The solution covers containerization, CI/CD automation, Kubernetes deployment design, monitoring,
and security best practices.

The application exposes two REST endpoints:
- `GET /health` – service health check
- `GET /predict` – returns a sample prediction score `{ "score": 0.75 }`

---

## Architecture Overview

**High-Level Flow:**

Developer → GitHub → CI/CD Pipeline (Jenkins) → Docker Hub  
→ Kubernetes Cluster (EKS / Local) → Monitoring & Alerts

---

## 1. Application & Containerization

### Technology Stack
- Language: Python (FastAPI)
- Container: Docker (multi-stage build)
- Runtime: Non-root container user
- Health Check: Docker + Kubernetes probes

### Docker Features
- Multi-stage Dockerfile
- Non-root execution
- Exposed health endpoint
- Lightweight base image

---

## 2. CI/CD Pipeline (Jenkins)

### CI Steps
- Source code checkout from GitHub
- Application test execution
- Docker image build
- Docker image push to Docker Hub

### CD Steps
- Kubernetes manifests prepared for deployment
- Supports rolling update strategy
- Designed for EKS / KIND / Docker Desktop Kubernetes

---

## 3. Kubernetes Deployment

### Kubernetes Resources
- Deployment (replicas, rolling update)
- Service (ClusterIP / NodePort)
- Liveness & Readiness probes
- Resource requests & limits

### Deployment Status
Due to Docker Desktop Kubernetes cluster initialization issues on the local system,
live deployment could not be completed within the assignment timeline.

However:
- All Kubernetes manifests are production-ready
- Manifests are compatible with AWS EKS and KIND clusters
- Rolling updates and health checks are fully configured

---

## 4. Monitoring & Alerts (Design)

### Metrics
- CPU utilization
- Memory utilization
- Pod restart count
- Health check failures

### Dashboard
Monitoring is designed using:
- AWS CloudWatch Container Insights (for EKS)
- OR Grafana dashboards

### Alerts Configured
| Alert Type | Threshold |
|----------|-----------|
High CPU Usage | >70% for 5 minutes |
High Memory Usage | >80% |
Health Check Failure | Liveness probe failure |

---

## 5. Security Best Practices

- Least-privilege IAM roles (for EKS / CI)
- No credentials stored in GitHub repository
- Secrets managed via AWS Secrets Manager / SSM (design)
- HTTPS enforced via Ingress / Load Balancer (production design)
- Container runs as non-root user

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
