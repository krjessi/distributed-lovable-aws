# Enterprise CI/CD Deployment, DevSecOps & Monitoring of Microservices on Kubernetes (AWS)

An end-to-end DevOps, DevSecOps, and observability project for building, securing, containerizing, deploying, and monitoring Spring Boot microservices on Kubernetes using AWS EKS.

## Technology Stack

| Category | Technology |
|---|---|
| Cloud | AWS |
| Kubernetes | Amazon EKS |
| Containerization | Docker |
| Orchestration | Kubernetes |
| Package Management | Helm |
| CI/CD | Jenkins, GitHub Actions |
| Build | Maven |
| Code Quality | SonarQube |
| Dependency Security | OWASP Dependency-Check |
| Container Security | Trivy |
| Container Registry | Amazon ECR |
| Monitoring | Prometheus, Grafana |
| Cloud Monitoring | Amazon CloudWatch |
| Infrastructure as Code | Terraform |
| Operating System | Linux |
| Scripting | Python |
| Application | Spring Boot Microservices |

---

## Architecture

```text
                         Developer
                             │
                             ▼
                          GitHub
                             │
                      Webhook / Trigger
                             │
                             ▼
                    Jenkins / GitHub Actions
                             │
                             ▼
                       Source Checkout
                             │
                             ▼
                       Maven Build
                             │
              ┌──────────────┴──────────────┐
              │                             │
              ▼                             ▼
         Unit Testing                 OWASP Dependency-Check
              │                             │
              │                     CVE / Dependency Scan
              │                             │
              └──────────────┬──────────────┘
                             ▼
                         SonarQube
                             │
                       Code Quality
                             │
                             ▼
                       Docker Build
                             │
                             ▼
                           Trivy
                             │
                    Container Image Scan
                             │
                             ▼
                         Amazon ECR
                             │
                             ▼
                         Helm Deploy
                             │
                             ▼
                      Amazon EKS
                             │
                ┌────────────┴────────────┐
                │                         │
                ▼                         ▼
          Health Checks              Smoke Tests
                │                         │
                └────────────┬────────────┘
                             ▼
                       Monitoring
                             │
                ┌────────────┼────────────┐
                ▼            ▼            ▼
           Prometheus      Grafana     CloudWatch
```

---

# 1. Project Overview

This project demonstrates an enterprise-style CI/CD, DevSecOps, Kubernetes, AWS, and monitoring workflow for Spring Boot microservices.

The implementation covers:

- Source code management with GitHub
- CI/CD automation with Jenkins and GitHub Actions
- Maven build and unit testing
- Static code-quality analysis with SonarQube
- Dependency vulnerability scanning with OWASP Dependency-Check
- Docker image creation
- Container image scanning with Trivy
- Image publishing to Amazon ECR
- Kubernetes deployment using Helm
- Application health checks
- Smoke testing
- Monitoring with Prometheus, Grafana, and Amazon CloudWatch
- Kubernetes troubleshooting and RCA

---

# 2. CI/CD Pipeline

The CI/CD pipeline automates the software delivery process from source checkout through Kubernetes deployment and validation.

## Pipeline Flow

```text
GitHub
   │
   ▼
Jenkins / GitHub Actions
   │
   ▼
Source Checkout
   │
   ▼
Maven Build
   │
   ├── Unit Testing
   │
   └── OWASP Dependency-Check
   │
   ▼
SonarQube
   │
   ▼
Docker Build
   │
   ▼
Trivy Image Scan
   │
   ▼
Amazon ECR
   │
   ▼
Helm Deployment
   │
   ▼
Amazon EKS
   │
   ├── Health Checks
   └── Smoke Tests
   │
   ▼
Monitoring
```

## CI/CD Stages

### Source Checkout

The pipeline retrieves application source code from GitHub.

### Maven Build

Maven is used to compile and package Spring Boot applications.

```text
Source Code
    ↓
Maven Build
    ↓
Application JAR
```

### Unit Testing

Unit tests are executed as part of the CI process before deployment.

### OWASP Dependency-Check

OWASP Dependency-Check is used to identify known vulnerabilities in third-party dependencies and report associated CVEs.

### SonarQube

SonarQube is used for source-code quality analysis and identification of code-quality and security-related findings.

### Docker Build

The Spring Boot application is packaged into a Docker image.

### Trivy

Trivy scans the Docker image for known container and image vulnerabilities before publishing.

### Amazon ECR

Validated Docker images are published to Amazon Elastic Container Registry.

### Helm Deployment

Helm is used to deploy the application to Kubernetes running on Amazon EKS.

### Health Checks

Post-deployment health checks validate application availability.

### Smoke Tests

Smoke tests provide basic post-deployment validation before the deployment is considered successful.

---

# 3. Kubernetes Deployment

Spring Boot microservices are containerized with Docker and deployed to Amazon EKS using Kubernetes and Helm.

Kubernetes resources used include:

- Deployments
- Services
- Ingress
- ConfigMaps
- Secrets
- Resource limits
- Health probes
- Horizontal Pod Autoscaler (HPA)

## Deployment Flow

```text
Amazon ECR
    │
    ▼
   Helm
    │
    ▼
Amazon EKS
    │
    ├── Deployments
    ├── Services
    ├── Ingress
    ├── ConfigMaps
    ├── Secrets
    ├── Health Probes
    ├── Resource Limits
    └── HPA
```

---

# 4. DevSecOps

Security controls are integrated into the CI/CD lifecycle.

```text
Code
 │
 ├── Unit Tests
 ├── OWASP Dependency-Check
 ├── SonarQube
 ├── Docker Build
 └── Trivy
       │
       ▼
     Amazon ECR
       │
       ▼
     Amazon EKS
```

| Tool | Purpose |
|---|---|
| SonarQube | Code quality and analysis |
| OWASP Dependency-Check | Dependency vulnerability scanning |
| Trivy | Container/image vulnerability scanning |

The objective is to identify quality and security risks before deployment.

---

# 5. Monitoring & Observability

Monitoring is implemented using Prometheus, Grafana, and Amazon CloudWatch.

## Monitoring Architecture

```text
                     Kubernetes
                         │
             ┌───────────┴───────────┐
             │                       │
             ▼                       ▼
        Applications           Kubernetes Resources
             │                       │
             └───────────┬───────────┘
                         ▼
                    Prometheus
                         │
                         ▼
                      Grafana


                  AWS Environment
                         │
                         ▼
                    CloudWatch
```

Monitoring covers:

- Application health
- Kubernetes resources
- CPU utilization
- Memory utilization
- Pod failures
- Deployment behavior

Prometheus collects metrics, Grafana provides dashboards and visualization, and CloudWatch provides AWS-level monitoring.

---

# 6. Incident Simulation & Troubleshooting

Production-style incidents are simulated and investigated using Kubernetes troubleshooting and RCA practices.

Scenarios include:

- Pod failures
- CrashLoopBackOff
- Image-pull failures
- Resource exhaustion
- Configuration issues
- Failed deployments

## Troubleshooting Flow

```text
Incident
   │
   ▼
Check Pod Status
   │
   ▼
Check Events
   │
   ▼
Check Logs
   │
   ▼
Check Deployment
   │
   ▼
Check Service
   │
   ▼
Check Configuration
   │
   ▼
Check Resources
   │
   ▼
Root Cause
   │
   ▼
Remediation
   │
   ▼
Redeploy
   │
   ▼
Health Check
   │
   ▼
Smoke Test
   │
   ▼
Validate Recovery
```

Useful commands:

```bash
kubectl get pods
kubectl describe pod <pod-name>
kubectl logs <pod-name>
kubectl get deployments
kubectl get services
kubectl get events
kubectl rollout status deployment/<deployment-name>
```

---

# 7. AWS EKS

Amazon EKS is used as the Kubernetes platform for deploying the microservices.

```text
                         AWS
                          │
                          ▼
                    Amazon EKS
                          │
              ┌───────────┴───────────┐
              │                       │
              ▼                       ▼
       Kubernetes Workloads      Monitoring
              │                       │
              ├── Microservices       ├── Prometheus
              ├── Services            ├── Grafana
              ├── Ingress             └── CloudWatch
              └── HPA
```

Container images are stored in Amazon ECR and consumed by Kubernetes during deployment.

---

# 8. Infrastructure as Code

Terraform is used for AWS infrastructure provisioning and management.

```text
Terraform
    │
    ▼
AWS Infrastructure
    │
    ├── Networking
    ├── Compute
    └── Kubernetes Infrastructure
```

Terraform allows infrastructure configuration to be maintained as code and reproduced consistently.

---

# 9. Linux & Python

Linux is used for application, infrastructure, and Kubernetes operations.

Python is used for automation and scripting tasks where required.

Typical activities include:

- System administration
- Kubernetes troubleshooting
- Automation
- Operational scripting
- Log analysis
- Deployment support

---

# 10. Project Validation

The deployment validation process follows:

```text
Build
  ↓
Unit Test
  ↓
Dependency Scan
  ↓
SonarQube
  ↓
Docker Build
  ↓
Trivy Scan
  ↓
ECR Push
  ↓
Helm Deploy
  ↓
EKS
  ↓
Health Check
  ↓
Smoke Test
  ↓
Monitoring
```

The objective is to validate the application across build, security, deployment, and post-deployment stages.

---

# 11. Key DevOps & SRE Practices

- Infrastructure as Code
- Automated CI/CD
- Continuous security scanning
- Containerization
- Kubernetes orchestration
- Helm-based deployments
- Health validation
- Smoke testing
- Application monitoring
- Kubernetes monitoring
- Incident troubleshooting
- Root cause analysis
- Deployment validation
- Production-oriented operational practices

---

# 12. Project Status

| Area | Status |
|---|---|
| Spring Boot Microservices | Implemented |
| Docker Containerization | Implemented |
| Kubernetes Deployment | Implemented |
| Helm | Implemented |
| Amazon EKS | Implemented |
| Amazon ECR | Implemented |
| Jenkins | Implemented / Integrated |
| GitHub Actions | Implemented / Integrated |
| Maven | Implemented |
| SonarQube | Implemented / Integrated |
| OWASP Dependency-Check | Implemented / Integrated |
| Trivy | Implemented / Integrated |
| Prometheus | Implemented |
| Grafana | Implemented |
| CloudWatch | Implemented |
| Terraform | Implemented |
| Linux | Used |
| Python | Used |
| Incident Simulation | Implemented |
| Kubernetes Troubleshooting / RCA | Implemented |

---

# 13. Author

**Mukesh Kumar**

DevOps / SRE Engineer

This project demonstrates an enterprise-style CI/CD, DevSecOps, Kubernetes, AWS, infrastructure-as-code, monitoring, and SRE troubleshooting workflow.
