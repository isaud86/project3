# README - Coworking Space Service Extension

## Overview

This repository contains the necessary files and instructions for deploying the Coworking Space Service Extension, which provides analytics data on user activity through APIs. This service is implemented following a microservice architecture pattern and is intended for deployment on a Kubernetes cluster named "project3" with a PostgreSQL database.

## Getting Started

### Prerequisites

Ensure the following tools and environments are set up locally:

- Python 3.6+
- Docker CLI
- `kubectl` for interacting with Kubernetes
- Helm for deploying chart packages in Kubernetes
- AWS CLI and configured credentials

### Dependencies

#### Local Environment

1. **Python Environment:** Ensure Python 3.6 or higher is installed.
2. **Docker:** Needed for building and running Docker containers.
3. **kubectl:** Command-line tool for Kubernetes cluster management.
4. **Helm:** Used for managing Kubernetes applications.

#### Remote Resources

1. **AWS CodeBuild:** For building Docker images in the cloud.
2. **AWS ECR:** Docker container registry for storing built images.
3. **Kubernetes (AWS EKS):** Cluster management for deployment.
4. **AWS CloudWatch:** For monitoring and logging services in EKS.
5. **GitHub:** Source code management.

### Setup

#### 1. Configure a PostgreSQL Database

- **Add Bitnami Helm repository:**
  ```bash
  helm repo add bitnami https://charts.bitnami.com/bitnami
  ```
- **Install PostgreSQL using Helm:**
  ```bash
  helm install postgres bitnami/postgresql --namespace default
  ```
  This command deploys PostgreSQL on the "project3" Kubernetes cluster. Verify the deployment by checking the service:
  ```bash
  kubectl get svc postgres-postgresql.default.svc.cluster.local
  ```
- **Retrieve the PostgreSQL password:**
  ```bash
  export POSTGRES_PASSWORD=$(kubectl get secret --namespace default postgres-postgresql -o jsonpath="{.data.postgres-password}" | base64 --decode)
  echo $POSTGRES_PASSWORD
  ```

#### 2. Running the Analytics Application Locally

- Navigate to the `analytics/` directory.
- **Install dependencies:**
  ```bash
  pip install -r requirements.txt
  ```
- **Run the application:**
  ```bash
  DB_USERNAME=postgres DB_PASSWORD=$POSTGRES_PASSWORD python app.py
  ```

### Project Instructions

1. Set up a PostgreSQL database using a Helm chart.
2. Create a Dockerfile for the Python application.
3. Configure a build pipeline with AWS CodeBuild.
4. Define Kubernetes service and deployment YAML configurations for deployment.
5. Monitor the deployment using AWS CloudWatch.

### Deliverables

- `Dockerfile`
- Screenshots of AWS CodeBuild pipeline, AWS ECR repository, and Kubernetes service (`kubectl get svc`), pods (`kubectl get pods`), and detailed views (`kubectl describe svc postgres-postgresql` and `kubectl describe deployment your-service-name`).
- Kubernetes configuration files (YAML).
- AWS CloudWatch logs.
- Comprehensive README.md documenting the deployment process.

### Stand Out Suggestions

1. **Resource Allocation:** Include memory and CPU limits in the Kubernetes deployment to ensure efficient resource use.
2. **AWS Instance Type:** Recommend a suitable AWS instance type for the application considering the resource needs and expected load.
3. **Cost Optimization:** Discuss strategies for cost reduction, such as using reserved instances or scaling down during off-peak hours.

### Best Practices

- Utilize a suitable base image in the Dockerfile and clearly comment complex commands.
- Adhere to semantic versioning for Docker images to track changes and upgrades efficiently.

---

This README file serves as both a guide for developers and a document for users to understand the setup and deployment process of the Coworking Space Service Extension on Kubernetes. Adjust paths and names as necessary to match your actual project setup and Kubernetes configurations.
