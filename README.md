# Retail DevOps CI/CD Pipeline Project

## Project Overview

This project demonstrates a complete DevOps CI/CD pipeline for deploying a Java Maven web application using modern DevOps tools and AWS Cloud.

The application is containerized using Docker, automated with Jenkins, deployed on Kubernetes (Minikube), configured using Ansible, and monitored with Prometheus and Grafana.

---

## Architecture

Developer
↓
GitHub Repository
↓
Jenkins Pipeline
↓
Maven Build
↓
Docker Image Build
↓
DockerHub Push
↓
Kubernetes Deployment
↓
Application Running
↓
Prometheus Monitoring
↓
Grafana Dashboard

---

## Technologies Used

- AWS EC2 (Ubuntu)
- Git & GitHub
- Maven
- Java
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
├── pom.xml
├── Dockerfile
├── Jenkinsfile
├── deployment.yaml
├── service.yaml
├── ansible/
│   ├── inventory
│   └── docker-deploy.yml
├── .gitignore
└── README.md
```

---

## CI/CD Pipeline

1. Developer pushes code to GitHub
2. Jenkins pulls latest source code
3. Maven builds the application
4. Docker builds the image
5. Docker image pushed to DockerHub
6. Kubernetes deploys application
7. Prometheus collects metrics
8. Grafana displays monitoring dashboard

---

## Docker Commands

Build Image

```
docker build -t thankidivyesh/abctehnologies:latest .
```

Run Container

```
docker run -d -p 8080:8080 thankidivyesh/abctehnologies:latest
```

---

## Kubernetes Commands

Deployment

```
kubectl apply -f deployment.yaml
```

Service

```
kubectl apply -f service.yaml
```

Check Pods

```
kubectl get pods
```

Check Services

```
kubectl get svc
```

---

## Ansible Deployment

Inventory

```
ansible/inventory
```

Run Playbook

```
ansible-playbook -i ansible/inventory ansible/docker-deploy.yml
```

---

## Monitoring

### Prometheus

Collects Kubernetes and Application Metrics.

### Grafana

Visualizes Metrics using Dashboards.

---

## Project Features

- Continuous Integration
- Continuous Deployment
- Docker Containerization
- Kubernetes Deployment
- Infrastructure Automation
- Monitoring using Prometheus
- Dashboard using Grafana

---

## Future Enhancements

- Terraform
- ArgoCD
- SonarQube
- Trivy
- Nexus
- AWS EKS

---

## 👨‍💻 Author

**Thanki Divyesh**

📧 Email: thankidivyesh@zohomail.in

🔗 GitHub: https://github.com/thankidivyesh
