Health API Automation Project
🎯 Objective

This project demonstrates the ability to automate cloud deployments, containerize services, implement monitoring, and apply DevOps best practices in a healthcare technology environment.

🧩 Assignment Summary

1. Containerize & Deploy a Simple Service

API created in Python (Flask) with two endpoints:

GET /health → returns status OK

GET /predict → returns { "score": 0.75 }

Dockerfile Highlights:

Multi-stage build

Non-root user

Healthcheck included

Dependencies installed via requirements.txt

Dockerfile Example Snippet:

FROM python:3.10-slim AS build
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

FROM python:3.10-slim
WORKDIR /app
COPY --from=build /usr/local/lib/python3.10/site-packages /usr/local/lib/python3.10/site-packages
COPY app /app
USER appuser
HEALTHCHECK CMD curl --fail http://localhost:5000/health || exit 1
CMD ["python", "app.py"]


2. Minimal CI/CD Pipeline (Jenkins)

CI Stages Implemented:

Checkout code from GitHub

Build Docker image

Push image to Docker Hub

Pipeline Snippet (Jenkinsfile):

pipeline {
    agent any
    environment {
        DOCKER_USER = credentials('docker-username')
        DOCKER_PASS = credentials('docker-password')
    }
    stages {
        stage('Checkout') {
            steps { git 'https://github.com/vaibhaoy19/Azodha_Flutter_mobile_App.git' }
        }
        stage('Build Docker Image') {
            steps { sh 'docker build -t vaibhaodocker19/health-api:latest .' }
        }
        stage('Push Docker Image') {
            steps {
                sh 'docker login -u $DOCKER_USER -p $DOCKER_PASS'
                sh 'docker push vaibhaodocker19/health-api:latest'
            }
        }
    }
}


✅ Status: Successfully implemented and tested on Jenkins.

⚠️ CD / Deployment: Kubernetes deployment stage failed; EKS cluster not yet created.

3. Basic Monitoring

CloudWatch Metrics Planned: CPU, Memory, Error count

Dashboard: Pending (to be created in CloudWatch/Grafana)

Alerts Planned: High CPU/memory usage, health check failures

4. Security Considerations

IAM: Least-privilege principle will be applied

Secrets: Stored in AWS Secrets Manager or SSM Parameter Store

Repository: No credentials included in code

HTTPS Enforcement: Planned explanation for API HTTPS enforcement

📂 Project Structure
health-api/
│
├── app/                 # Python Flask API code
├── requirements.txt     # Python dependencies
├── Dockerfile           # Container build instructions
├── Jenkinsfile          # CI/CD pipeline
└── README.md

📈 CI/CD Workflow

Developer pushes code to GitHub

Jenkins pipeline triggers automatically

Code is built and tested

Docker image is built and pushed to Docker Hub

(Pending) Deployment to Kubernetes cluster (EKS)

📝 Notes / Pending Work

Kubernetes deployment manifest & EKS cluster creation

CloudWatch / Grafana dashboard & alerts

Full security enforcement configuration

📦 Submission

GitHub Repo: [Link to your repo]

IaC Code: (Pending Kubernetes manifests / Terraform)

Screenshots: Jenkins pipeline success captured; other pending

Prepared By: Vaibhao Yenchalwar
