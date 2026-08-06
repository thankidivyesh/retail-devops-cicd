# Retail DevOps CI/CD Pipeline Project

## Project Overview

This project demonstrates a complete DevOps CI/CD pipeline for deploying a Java Maven web application using modern DevOps tools on AWS Cloud.

The application is containerized using Docker, automated with Jenkins, deployed on Kubernetes (Minikube), configured using Ansible, and monitored using Prometheus and Grafana.

---

## Architecture

```
Developer
    │
    ▼
GitHub Repository
    │
    ▼
Jenkins Pipeline
    │
    ▼
Maven Build
    │
    ▼
Docker Image Build
    │
    ▼
DockerHub Push
    │
    ▼
Kubernetes Deployment
    │
    ▼
Application Running
    │
    ▼
Prometheus Monitoring
    │
    ▼
Grafana Dashboard
```

---

## Technologies Used

- AWS EC2 (Ubuntu)
- Git & GitHub
- Java
- Maven
- Jenkins
- Docker
- DockerHub
- Kubernetes
- Minikube
- Ansible
- Helm
- Prometheus
- Grafana

---

## Project Structure

```
retail-devops-cicd/
│
├── src/
├── ansible/
│   ├── inventory
│   └── docker-deploy.yml
├── screenshots/
├── Dockerfile
├── Jenkinsfile
├── deployment.yaml
├── service.yaml
├── pom.xml
├── README.md
└── .gitignore
```

---

## CI/CD Pipeline

1. Developer pushes code to GitHub.
2. Jenkins pulls the latest source code.
3. Maven builds and packages the application.
4. Docker builds the application image.
5. Docker image is pushed to DockerHub.
6. Kubernetes deploys the application.
7. Prometheus collects application metrics.
8. Grafana displays monitoring dashboards.

---

## Docker Commands

### Build Docker Image

```bash
docker build -t thankidivyesh/abctechnologies:latest .
```

### Run Docker Container

```bash
docker run -d -p 8080:8080 thankidivyesh/abctechnologies:latest
```

---

## Kubernetes Commands

### Deploy Application

```bash
kubectl apply -f deployment.yaml
```

### Create Service

```bash
kubectl apply -f service.yaml
```

### Check Pods

```bash
kubectl get pods
```

### Check Services

```bash
kubectl get svc
```

---

## Ansible Deployment

### Inventory

```text
ansible/inventory
```

### Run Playbook

```bash
ansible-playbook -i ansible/inventory ansible/docker-deploy.yml
```

---

## Monitoring

### Prometheus

- Collects Kubernetes and application metrics.
- Monitors CPU, Memory, Network and Node Exporter metrics.

### Grafana

- Visualizes Prometheus metrics.
- Displays dashboards for Kubernetes and system monitoring.

---

## Project Features

- Continuous Integration (CI)
- Continuous Deployment (CD)
- Docker Containerization
- Kubernetes Deployment
- Infrastructure Automation with Ansible
- Monitoring using Prometheus
- Dashboard Visualization using Grafana

---

## Screenshots

Project screenshots are available inside the **screenshots/** folder.

- GitHub Repository
- Jenkins Pipeline
- Docker Images
- Kubernetes Pods
- Kubernetes Services
- Prometheus Dashboard
- Grafana Dashboard
- Application Output

---

## Future Enhancements

- Terraform
- ArgoCD
- SonarQube
- Trivy
- Nexus Repository
- AWS EKS

---

## Author

**Thanki Divyesh**

📧 Email: thankidivyesh@zohomail.in

📍 Location: Jamnagar,Gujarat, India

🔗 GitHub Repository:

https://github.com/thankidivyesh/retail-devops-cicd

🔗 LinkedIn:
https://linkedin.com/in/thanki-divyesh-10422341b
