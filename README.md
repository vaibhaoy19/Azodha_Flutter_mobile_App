Health API Automation Project 🎯
Objective

This project demonstrates automation of cloud deployments, containerization of services, CI/CD pipelines, monitoring, and security best practices in a healthcare technology environment.

🌟 Project Overview
1. Containerized Service

A small API created in Python (Flask) with the following endpoints:

Endpoint	Response
GET /health	{"status": "OK"}
GET /predict	{"score": 0.75}

Dockerfile Highlights:

Multi-stage build

Runs as non-root user

Healthcheck enabled

Dependencies installed via requirements.txt

Dockerfile Example:

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

2. CI/CD Pipeline (Jenkins)

Implemented Stages:

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


Status: ✅ Successfully built and pushed Docker image.
Pending: CD / Deployment to Kubernetes cluster (EKS not created yet).

3. Monitoring

Planned Monitoring:

Metrics: CPU, Memory, Error count

Dashboard: CloudWatch / Grafana

Alerts: High CPU/memory usage, health check failures

4. Security Considerations

IAM: Least-privilege roles

Secrets: Stored in AWS Secrets Manager / SSM

Code Repository: No credentials included

HTTPS: API enforcement planned

5. Project Structure
health-api/
│
├── app/                 # Flask API code
├── requirements.txt     # Python dependencies
├── Dockerfile           # Container instructions
├── Jenkinsfile          # CI/CD pipeline
└── README.md

6. CI/CD Workflow Diagram
[GitHub Push] --> [Jenkins CI Pipeline]
                  |--> Build & Test
                  |--> Docker Image Build
                  |--> Push to Docker Hub
                  |--> (Pending) Deploy to Kubernetes

7. Pending Work

Kubernetes deployment (EKS cluster)

CloudWatch / Grafana dashboard & alerts

Full security enforcement & HTTPS

8. Submission

GitHub Repo: [Link to repo]

IaC Code: Pending Kubernetes manifests / Terraform

Screenshots: Jenkins pipeline success (Docker build & push completed)

Prepared By: Vaibhao Yenchalwar
Date: 3rd January 2026Health API Automation Project
🎯 Objective

This project demonstrates automation of cloud deployments, containerization of services, CI/CD pipelines, monitoring, and security best practices in a healthcare technology environment.

🧩 Project Overview
1. Containerized Service

A small API created in Python (Flask) with the following endpoints:

Endpoint	Response
GET /health	{"status": "OK"}
GET /predict	{"score": 0.75}

Dockerfile Highlights:

Multi-stage build

Runs as non-root user

Healthcheck enabled

Dependencies installed via requirements.txt

Dockerfile Example:

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

2. CI/CD Pipeline (Jenkins)

Implemented Stages:

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


Status: ✅ Successfully built and pushed Docker image.
Pending: CD / Deployment to Kubernetes cluster (EKS not created yet).

3. Monitoring

Planned Monitoring:

Metrics: CPU, Memory, Error count

Dashboard: CloudWatch / Grafana

Alerts: High CPU/memory usage, health check failures

4. Security Considerations

IAM: Least-privilege roles

Secrets: Stored in AWS Secrets Manager / SSM

Code Repository: No credentials included

HTTPS: API enforcement planned

5. Project Structure
health-api/
│
├── app/                 # Flask API code
├── requirements.txt     # Python dependencies
├── Dockerfile           # Container instructions
├── Jenkinsfile          # CI/CD pipeline
└── README.md

6. CI/CD Workflow Diagram
[GitHub Push] --> [Jenkins CI Pipeline]
                  |--> Build & Test
                  |--> Docker Image Build
                  |--> Push to Docker Hub
                  |--> (Pending) Deploy to Kubernetes

7. Pending Work

Kubernetes deployment (EKS cluster)

CloudWatch / Grafana dashboard & alerts

Full security enforcement & HTTPS

8. Submission

GitHub Repo: [Link to repo]

IaC Code: Pending Kubernetes manifests / Terraform

Screenshots: Jenkins pipeline success (Docker build & push completed)

Prepared By: Vaibhao Yenchalwar
