# Health API DevOps Project

🎯 **Objective:**  
Automate cloud deployments, containerize services, implement CI/CD, and apply DevOps best practices for a simple healthcare API service.

---

## 1. Project Overview

This project demonstrates the DevOps workflow for a simple Python-based API with two endpoints:

- `GET /health` → Returns API health status  
- `GET /predict` → Returns `{ "score": 0.75 }`  

**Implemented so far:**

1. Containerization using Docker (production-grade image)  
2. Jenkins-based CI pipeline for automated build and Docker push  
3. Minimal CI/CD structure (deployment to Kubernetes pending)  

**Pending:**  
- Kubernetes deployment (EKS/Minikube)  
- Monitoring & alert dashboards (CloudWatch/Grafana)  
- Security hardening (IAM, Secrets, HTTPS)

---

## 2. Architecture Diagram

