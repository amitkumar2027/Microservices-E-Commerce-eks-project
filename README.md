<div align="center">

# 🛒 Production-Ready E-Commerce Microservices on Amazon EKS

### Cloud-Native • Containerized • Secure • Observable • GitOps-Driven

[![Amazon EKS](https://img.shields.io/badge/Amazon-EKS-FF9900?logo=amazoneks&logoColor=white)](https://aws.amazon.com/eks/)
[![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?logo=kubernetes&logoColor=white)](https://kubernetes.io/)
[![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)](https://www.docker.com/)
[![Terraform](https://img.shields.io/badge/Terraform-844FBA?logo=terraform&logoColor=white)](https://www.terraform.io/)
[![Argo CD](https://img.shields.io/badge/Argo%20CD-EF7B4D?logo=argo&logoColor=white)](https://argo-cd.readthedocs.io/)
[![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?logo=githubactions&logoColor=white)](https://github.com/features/actions)
[![Jenkins](https://img.shields.io/badge/Jenkins-D24939?logo=jenkins&logoColor=white)](https://www.jenkins.io/)
[![SonarQube](https://img.shields.io/badge/SonarQube-4E9BCD?logo=sonarqube&logoColor=white)](https://www.sonarsource.com/products/sonarqube/)
[![Trivy](https://img.shields.io/badge/Trivy-1904DA?logo=aquasecurity&logoColor=white)](https://trivy.dev/)
[![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?logo=prometheus&logoColor=white)](https://prometheus.io/)
[![Grafana](https://img.shields.io/badge/Grafana-F46800?logo=grafana&logoColor=white)](https://grafana.com/)
[![Amazon Route 53](https://img.shields.io/badge/Route%2053-8C4FFF?logo=amazonroute53&logoColor=white)](https://aws.amazon.com/route53/)

<br/>

**A production-oriented e-commerce platform deployed on Amazon EKS using Kubernetes, Infrastructure as Code, CI/CD automation, GitOps, security scanning, and Kubernetes observability.**

</div>

---

## 📌 Project Overview

This project demonstrates an end-to-end **cloud-native microservices e-commerce deployment** on **Amazon Elastic Kubernetes Service (EKS)**.

The application is decomposed into independent services such as **Frontend, Checkout, Product Catalog, Cart, Recommendation, Payment, Shipping, Currency, Email, and Advertisement** services. The platform uses containers for application packaging and Kubernetes for service orchestration.

The infrastructure and delivery workflow are automated using **Terraform, GitHub Actions/Jenkins, Docker, SonarQube, Trivy, Docker Hub, Argo CD, and Kubernetes**. Public traffic is routed through **Amazon Route 53 → Application Load Balancer → Kubernetes Ingress/Services**, while application metrics are collected through **Prometheus and Grafana**.

### 🎯 Key Goals

- Deploy a multi-service e-commerce application on Amazon EKS
- Automate infrastructure provisioning with Terraform
- Build and scan container images
- Implement CI/CD and GitOps-based continuous delivery
- Maintain Kubernetes manifests as the deployment source of truth
- Expose the application through AWS networking components
- Add code-quality and container-security checks
- Monitor Kubernetes workloads and application health
- Demonstrate a scalable, production-style DevOps workflow

---

# 🧰 TECHNOLOGY STACK

| Category | Technologies |
|---|---|
| ☁️ **Cloud** | **AWS**, Amazon EKS, EC2 / EKS managed compute, Route 53, Application Load Balancer |
| ☸️ **Container Orchestration** | **Kubernetes**, EKS, Pods, Services, Ingress |
| 📦 **Containers** | **Docker**, Docker Hub |
| 🏗️ **Infrastructure as Code** | **Terraform** |
| 🔄 **CI/CD** | **GitHub Actions, Jenkins** |
| 🚀 **GitOps / CD** | **Argo CD** |
| 🔍 **Code Quality** | **SonarQube** |
| 🛡️ **Container Security** | **Trivy** |
| 📊 **Monitoring** | **Prometheus, Grafana** |
| 🌐 **Networking / DNS** | **Route 53, Application Load Balancer, Kubernetes Services / Ingress** |
| 🔐 **Kubernetes Security / Configuration** | **Kubernetes Secrets, Configurations, Persistent Volumes / PVCs** |
| 🗄️ **Application Data / Caching** | **Redis Cache, Database Service** |
| 💻 **Development** | **Visual Studio Code, Git, GitHub** |

---

# 🏗️ HIGH-LEVEL ARCHITECTURE

The application consists of multiple independently deployable microservices.

![Microservices Architecture](./images/Project%20Architecture.png)
### 🔹 Microservices Flow

**User / Load Generator → Frontend → Backend Microservices → Data / Cache**

The main application flow is:

1. **User** sends an HTTP request to the **Frontend**.
2. The **Load Generator** can also generate HTTP traffic for testing.
3. The **Frontend** communicates with backend services.
4. **Checkout** coordinates purchase-related operations.
5. **Product Catalog** provides product information.
6. **Recommendation** generates product recommendations.
7. **Cart** manages shopping-cart operations.
8. **Redis Cache** is used by the cart layer for fast access.
9. **Payment** processes payment-related operations.
10. **Shipping** handles shipping-related operations.
11. **Currency** provides currency conversion functionality.
12. **Email** handles notification/email operations.
13. **Ad** provides advertisement-related functionality.

This separation allows individual services to be developed, deployed, scaled, and monitored independently.

---

# 🔄 CI/CD + GITOPS ARCHITECTURE

![CI/CD and EKS Architecture](docs/cicd-eks-architecture.png)

The delivery pipeline automates the journey from **source code → quality checks → container image → security scan → GitOps deployment → EKS**.

### 🔁 Complete Pipeline Flow

```text
Developer
   │
   ▼
GitHub Repository
   │
   ▼
GitHub Actions / Jenkins
   │
   ├── Dependency Check
   │
   ├── SonarQube Code Quality Analysis
   │
   ├── Docker Build
   │
   ├── Push Image → Docker Hub
   │
   └── Trivy Image Scan
           │
           ▼
     Update Kubernetes
       Deployment File
           │
           ▼
       Git Repository
           │
           ▼
         Argo CD
           │
           ▼
      Amazon EKS Cluster
           │
     ┌─────┼───────────────┐
     ▼     ▼               ▼
 Frontend Backend       Database
     │     │               │
     └─────┴───────────────┘
           │
           ▼
      Application
```

---

# 🚀 END-TO-END REQUEST FLOW

```text
                         INTERNET USER
                              │
                              ▼
                     ┌─────────────────┐
                     │  Amazon Route 53│
                     │      DNS        │
                     └────────┬────────┘
                              │
                              ▼
                 ┌─────────────────────────┐
                 │ Application Load Balancer│
                 │          (ALB)           │
                 └────────────┬────────────┘
                              │
                              ▼
                       Kubernetes Ingress
                              │
                              ▼
                    ┌───────────────────┐
                    │     Frontend      │
                    └─────────┬─────────┘
                              │
              ┌───────────────┼────────────────┐
              ▼               ▼                ▼
         Backend APIs     Checkout          Services
              │               │
              ▼               ▼
       ┌────────────┐   ┌────────────┐
       │ Product    │   │ Payment    │
       │ Catalog    │   │ Shipping   │
       └────────────┘   │ Currency   │
                        │ Email      │
                        └────────────┘
                              │
                              ▼
                       Database / Cache
```

---

# ⚙️ CI/CD PIPELINE

The project implements an automated delivery process designed to reduce manual deployment steps.

### 1. 👨‍💻 Source Code

Developers work locally using **VS Code**, commit changes, and push them to GitHub.

### 2. 🔄 Pipeline Trigger

A push or pull-request event triggers the CI/CD workflow through **GitHub Actions / Jenkins**.

### 3. 📦 Dependency Validation

Application dependencies are checked before creating a release artifact.

### 4. 🔍 Code Quality

**SonarQube** analyzes the application code for code-quality issues, bugs, vulnerabilities, and maintainability concerns.

### 5. 🐳 Docker Build

The application is packaged into a Docker image.

```bash
docker build -t ecommerce-service .
```

### 6. 📤 Container Registry

The image is pushed to **Docker Hub**.

```bash
docker push <dockerhub-username>/<image>:<tag>
```

### 7. 🛡️ Container Security Scan

**Trivy** scans the container image for known vulnerabilities before deployment.

```bash
trivy image <docker-image>:<tag>
```

### 8. 📝 Kubernetes Manifest Update

The pipeline updates the Kubernetes deployment configuration with the newly built image tag.

### 9. 🌿 GitOps Repository

The updated deployment manifest is committed back to Git.

### 10. 🚀 Argo CD Synchronization

**Argo CD** detects the Git change and synchronizes the desired state with the Amazon EKS cluster.

### 11. ☸️ Kubernetes Deployment

EKS creates/updates the required:

- Deployments
- Pods
- Services
- Ingress
- Configurations
- Secrets
- Persistent Volumes / PVCs

### 12. 📊 Observability

**Prometheus** collects metrics and **Grafana** provides dashboards for Kubernetes and application monitoring.

---

# ☁️ AWS INFRASTRUCTURE

The platform uses AWS services as the underlying cloud infrastructure.

### AWS Components

- **Amazon EKS** — Managed Kubernetes control plane and cluster platform
- **Amazon EC2 / EKS compute** — Runs Kubernetes workloads
- **Application Load Balancer** — Routes external HTTP/HTTPS traffic
- **Amazon Route 53** — DNS management and domain routing
- **AWS networking** — Provides connectivity between application components
- **Kubernetes Secrets** — Stores sensitive application configuration
- **Persistent Volumes / PVCs** — Provides persistent application storage where required

---

# 🏗️ INFRASTRUCTURE AS CODE WITH TERRAFORM

Terraform is used to provision and manage the cloud infrastructure in a repeatable way.

Typical workflow:

```bash
terraform init
terraform validate
terraform plan
terraform apply
```

Terraform helps maintain infrastructure as code, making environments easier to reproduce and changes easier to review.

---

# ☸️ KUBERNETES DEPLOYMENT

The application is organized into Kubernetes workloads representing the different microservices.

Example structure:

```text
EKS Cluster
│
├── Frontend
│   ├── Deployment
│   ├── Pods
│   └── Service
│
├── Backend
│   ├── Deployment
│   ├── Pods
│   └── Service
│
├── Database
│   ├── Deployment / Stateful Workload
│   ├── Pods
│   ├── Service
│   ├── PV
│   └── PVC
│
├── Ingress
│
├── Secrets
│
└── Monitoring
    ├── Prometheus
    └── Grafana
```

---

# 📈 MONITORING & OBSERVABILITY

The platform includes Kubernetes monitoring using:

### Prometheus

Prometheus collects time-series metrics from the Kubernetes environment and workloads.

Typical metrics include:

- CPU utilization
- Memory utilization
- Pod availability
- Container health
- Request metrics
- Resource consumption

### Grafana

Grafana visualizes collected metrics through dashboards.

```text
Kubernetes Workloads
        │
        ▼
   Metrics Export
        │
        ▼
   Prometheus
        │
        ▼
     Grafana
        │
        ▼
Monitoring Dashboards
```

---

# 🔐 SECURITY

Security is integrated into the delivery pipeline rather than being treated as a final deployment step.

### Security Measures

- **Trivy** container vulnerability scanning
- **SonarQube** code-quality/security analysis
- Kubernetes **Secrets** for sensitive configuration
- IAM-based AWS access control
- Controlled Kubernetes access
- Image-based deployment
- Git-based change tracking

> **Best practice:** credentials, AWS access keys, passwords, and other secrets should never be committed directly to the Git repository.

---

# 📂 RECOMMENDED PROJECT STRUCTURE

```text
Microservices-E-Commerce-eks-project/
│
├── 📁 ecr-terraform/              # ECR infrastructure
│   ├── backend.tf
│   ├── ecr-jenkinsfile
│   └── ecr-repo-main.tf
│
├── 📁 eks-terraform/              # EKS infrastructure
│   ├── backend.tf
│   ├── eks-jenkinsfile
│   ├── main.tf
│   └── variable.tf
│
├── 📁 jenkinsfiles/               # CI/CD pipelines
│   ├── adservice
│   ├── cartservice
│   ├── checkoutservice
│   ├── currencyservice
│   ├── emailservice
│   ├── frontend
│   ├── loadgenerator
│   ├── paymentservice
│   ├── productcatalogservice
│   ├── recommendationservice
│   ├── shippingservice
│   │
│   └── 📁 kubernetes-files/       # Kubernetes manifests
│       ├── adservice.yaml
│       ├── cartservice.yaml
│       ├── checkoutservice.yaml
│       ├── currencyservice.yaml
│       ├── emailservice.yaml
│       ├── frontend.yaml
│       ├── loadgenerator.yaml
│       ├── paymentservice.yaml
│       ├── productcatalogservice.yaml
│       ├── recommendationservice.yaml
│       ├── redis-cart.yaml
│       └── shippingservice.yaml
│
├── 📁 s3-buckets/                 # S3 infrastructure
│   ├── .terraform/
│   ├── .terraform.lock.hcl
│   ├── main.tf
│   ├── outputs.tf
│   ├── terraform.tfstate
│   ├── terraform.tfstate.backup
│   └── variables.tf
│
├── 📁 src/                        # Microservices source code
│   ├── adservice/
│   ├── cartservice/
│   ├── checkoutservice/
│   ├── currencyservice/
│   ├── emailservice/
│   ├── frontend/
│   ├── loadgenerator/
│   ├── paymentservice/
│   ├── productcatalogservice/
│   ├── recommendationservice/
│   └── shippingservice/
│
├── terraform_main_ec2              # EC2 Terraform configuration
├── .editorconfig                   # Editor configuration
├── .gitignore                      # Git ignored files
└── README.md                       # Project documentation
```

---

# 🛠️ SETUP & DEPLOYMENT

## Prerequisites

Install/configure the following tools:

```text
AWS CLI
kubectl
eksctl
Terraform
Docker
Git
Helm
Argo CD CLI
```

Also configure:

- AWS credentials
- GitHub repository
- Docker Hub account
- SonarQube
- Trivy
- EKS access permissions

---

## 1️⃣ Clone the Repository

```bash
git clone https://github.com/amitkumar2027/Microservices-E-Commerce-eks-project
cd Microservices-E-Commerce-eks-project
```

## 2️⃣ Provision Infrastructure

```bash
cd terraform

terraform init
terraform validate
terraform plan
terraform apply
```

## 3️⃣ Configure EKS Access

```bash
aws eks update-kubeconfig \
  --region <aws-region> \
  --name <eks-cluster-name>
```

Verify:

```bash
kubectl get nodes
```

## 4️⃣ Deploy Argo CD

Install Argo CD in the cluster:

```bash
kubectl create namespace argocd

kubectl apply \
  -n argocd \
  -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

Check:

```bash
kubectl get pods -n argocd
```

## 5️⃣ Apply GitOps Application

```bash
kubectl apply -f argocd/application.yaml
```

Argo CD will continuously reconcile the Kubernetes cluster with the manifests stored in Git.

## 6️⃣ Verify Workloads

```bash
kubectl get pods -A
kubectl get svc -A
kubectl get ingress -A
```

---

# 🔁 DEPLOYMENT LIFECYCLE

```text
CODE
 │
 ▼
GitHub
 │
 ▼
CI PIPELINE
 │
 ├── Dependency Check
 ├── SonarQube
 ├── Docker Build
 └── Trivy Scan
 │
 ▼
Docker Hub
 │
 ▼
Update Kubernetes Manifest
 │
 ▼
Git Repository
 │
 ▼
Argo CD
 │
 ▼
Amazon EKS
 │
 ▼
Kubernetes Pods
 │
 ▼
Production Application
```

---

# 🎯 PROJECT HIGHLIGHTS

- ✅ Microservices-based e-commerce architecture
- ✅ Amazon EKS deployment
- ✅ Infrastructure as Code with Terraform
- ✅ Docker containerization
- ✅ GitHub Actions / Jenkins CI automation
- ✅ SonarQube quality analysis
- ✅ Trivy container security scanning
- ✅ Docker Hub image registry
- ✅ Argo CD GitOps deployment
- ✅ Kubernetes Deployments and Services
- ✅ Route 53 DNS
- ✅ Application Load Balancer
- ✅ Prometheus monitoring
- ✅ Grafana dashboards
- ✅ Kubernetes Secrets and persistent storage
- ✅ Automated application delivery

---

# 💼 DEVOPS SKILLS DEMONSTRATED

This project demonstrates practical experience with:

```text
Cloud Computing
AWS
Amazon EKS
Kubernetes
Docker
Terraform
Git
GitHub
GitHub Actions
Jenkins
CI/CD
GitOps
Argo CD
SonarQube
Trivy
Docker Hub
Route 53
Application Load Balancer
Prometheus
Grafana
Linux
Infrastructure as Code
Container Security
Kubernetes Networking
Observability
```

---

# 📊 ARCHITECTURE SUMMARY

| Layer | Components |
|---|---|
| **Client** | User, Load Generator |
| **DNS** | Amazon Route 53 |
| **Traffic Entry** | Application Load Balancer |
| **Orchestration** | Amazon EKS / Kubernetes |
| **Application** | Frontend + Microservices |
| **Caching** | Redis |
| **Storage** | Database + PV/PVC |
| **CI** | GitHub Actions / Jenkins |
| **Quality** | SonarQube |
| **Containerization** | Docker |
| **Registry** | Docker Hub |
| **Security** | Trivy |
| **CD / GitOps** | Argo CD |
| **Monitoring** | Prometheus + Grafana |
| **IaC** | Terraform |

---

# 🧪 VALIDATION CHECKLIST

After deployment, verify:

```bash
# Cluster
kubectl get nodes

# Pods
kubectl get pods -A

# Services
kubectl get svc -A

# Ingress
kubectl get ingress -A

# Argo CD
kubectl get pods -n argocd

# Application health
kubectl describe pod <pod-name>

# Logs
kubectl logs <pod-name>
```

---

# 🏆 OUTCOME

The final platform provides a complete DevOps lifecycle:

**Develop → Commit → Analyze → Build → Scan → Push → Update Manifest → GitOps Sync → Deploy to EKS → Monitor**

This project combines **cloud infrastructure, containers, Kubernetes orchestration, CI/CD, GitOps, security, networking, and observability** into a single production-oriented workflow.

---

## 👨‍💻 Author

**Amit Kumar**

> Cloud & DevOps Enthusiast | AWS | Kubernetes | Docker | Terraform | CI/CD | GitOps

---

<div align="center">

### ⭐ If this project helped you learn Cloud & DevOps, consider starring the repository!

**Built with AWS • Kubernetes • Docker • Terraform • GitHub Actions • Jenkins • Argo CD • Prometheus • Grafana**

</div>


