# README - Coworking Space Service Extension

## Overview

This document outlines the deployment of the Coworking Space Service Extension, which facilitates analytics on user activity via a set of APIs. This application is structured using a microservices architecture and is designed for deployment on a Kubernetes cluster managed by AWS EKS, using PostgreSQL as a database backend.

## Getting Started

### Prerequisites

Before you start, ensure you have the following tools and accounts set up:

- Python 3.6 or higher
- Docker CLI
- `kubectl` configured with access to your Kubernetes cluster
- Helm 3
- AWS CLI with appropriate permissions

### Dependencies

#### Local Environment

- **Python Environment:** Python 3.6+ is required for running the analytics application.
- **Docker:** For building and running containerized applications.
- **kubectl:** For interacting with your Kubernetes cluster.
- **Helm:** For managing Kubernetes applications through Helm charts.

#### Remote Resources

- **AWS CodeBuild:** Builds Docker images based on your source code.
- **AWS ECR:** Hosts Docker images in a private Docker registry.
- **Kubernetes (AWS EKS):** Hosts your application in a managed Kubernetes environment.
- **AWS CloudWatch:** Monitors and logs activities within your applications.
- **GitHub:** Manages and stores version-controlled code.

### Setup

#### 1. Configure a PostgreSQL Database

- **Add Bitnami Helm repository:**
  ```bash
  helm repo add bitnami https://charts.bitnami.com/bitnami
  ```
- **Install PostgreSQL using Helm:**
  ```bash
  helm install postgres bitnami/postgresql --set persistence.storageClass=gp2,volumeSize=10Gi --namespace default
  ```
  This will provision a PostgreSQL database within your Kubernetes cluster. Verify the deployment:
  ```bash
  kubectl get svc postgres-postgresql
  ```

#### 2. Running the Analytics Application Locally

- Navigate to the `analytics/` directory.
- **Install dependencies:**
  ```bash
  pip install -r requirements.txt
  ```
- **Run the application:**
  ```bash
  DB_USERNAME=postgres DB_PASSWORD=$(kubectl get secret --namespace default postgres-postgresql -o jsonpath="{.data.postgres-password}" | base64 --decode) python app.py
  ```

### Cluster Configuration

#### AWS EKS Cluster Setup

1. **EKS Cluster Creation:**
   - Create a VPC and subnets.
   - Define an IAM role for EKS services.
   - Deploy an EKS cluster specifying the VPC and subnets.

2. **Node Group Configuration:**
   - Deploy EC2 instances as worker nodes.
   - Configure auto-scaling to manage load effectively.

3. **Security Configurations:**
   - Define IAM roles and policies for secure access.
   - Implement pod security policies and network policies to restrict traffic within the cluster.

#### PostgreSQL Setup

- **Helm Deployment:** Deploy PostgreSQL using the Bitnami chart for reliability and ease of management.
- **Security:** Manage credentials using Kubernetes secrets and limit database access to necessary Kubernetes services.

### Deployment Process

1. **Continuous Integration and Deployment:**
   - Use GitHub for source control.
   - Set up AWS CodeBuild to automate builds and tests.
   - Push successful builds to AWS ECR.

2. **Kubernetes Deployment:**
   - Write and apply Kubernetes YAML configurations for deployment and services.
   - Use Helm for easier management of releases.

3. **Monitoring:**
   - Set up AWS CloudWatch for application monitoring and logging.

### Deliverables

- `Dockerfile`
- Kubernetes configuration files
- Screenshots of the AWS services dashboard (ECR, CodeBuild)
- Logs and monitoring setup on AWS CloudWatch

### Best Practices

- Ensure all Kubernetes configurations follow security best practices.
- Use descriptive and clear comments in Dockerfiles and Kubernetes YAML files.
- Implement CI/CD pipelines that include linter, unit tests, and integration tests before deployment.

This README aims to provide a comprehensive guide for setting up and deploying the Coworking Space Service Extension on Kubernetes without the use of load balancers, focusing on internal cluster communication and security.

---

Adjust any specifics or add more detailed steps according to your project's requirements and AWS configurations. This README serves both as a deployment guide and a documentation tool for new developers or administrators working on the project.
