# Coworking Space Service

This project is part of the Udacity Cloud DevOps Engineer Nanodegree program. It focuses on building and deploying a microservice for managing a coworking space using Kubernetes and AWS services.

## Project Overview

The Coworking Space Service aims to create a scalable and reliable microservice that handles various functionalities related to managing a coworking space, such as user registration, booking management, and resource allocation.

## Technologies Used

- **Docker**: Containerization platform used to package the microservice.
- **AWS ECR**: Elastic Container Registry for storing Docker images.
- **AWS CodeBuild**: Continuous integration and deployment service for building and deploying the Docker image.
- **Kubernetes**: Container orchestration platform for managing and scaling the microservice.
- **AWS RDS**: Relational Database Service for hosting the Postgres database.
- **AWS CloudWatch**: Monitoring and logging service for tracking the application's health and performance.
- **Amazon EKS**: Fully managed Kubernetes service for running Kubernetes on AWS without needing to manage the underlying infrastructure.

## Project Setup

### Prerequisites

1. Install the AWS CLI version 2 on your local machine. Follow the [official AWS instructions](https://aws.amazon.com/cli/) for installation.

2. Configure AWS CLI:
   ```
   aws configure
   ```
   This will prompt you to enter your AWS Access Key ID, Secret Access Key, default region, and default output format.

3. Create an IAM role with the necessary permissions for EKS:
   - AmazonEKSClusterPolicy
   - AmazonEKSServicePolicy

4. Use the AWS CLI to create your EKS cluster:
   ```
   aws eks create-cluster --name <cluster-name> --role-arn <role-arn> --resources-vpc-config subnetIds=<subnet-ids>,securityGroupIds=<security-group-ids>
   ```

### Deploying the Microservice

1. Clone the project repository:
   ```
   git clone <repository-url>
   ```
2. Navigate to the project directory:
   ```
   cd coworking-space-service
   ```
3. Build the Docker image:
   ```
   docker build -t coworking-service .
   ```
4. Push the Docker image to AWS ECR:
   ```
   docker push <aws-ecr-repository-url>
   ```
5. Set up the Kubernetes cluster (EKS specifics):
   ```
   kubectl apply -f kubernetes/cluster.yaml
   ```
6. Deploy the microservice:
   ```
   kubectl apply -f kubernetes/deployment.yaml
   ```
7. Create the service:
   ```
   kubectl apply -f kubernetes/service.yaml
   ```
8. Set up the database service:
   ```
   kubectl apply -f kubernetes/database.yaml
   ```

## Usage

Utilize the microservice API via the service's external IP address and use the API endpoints for various actions, such as user registration, booking management, and resource allocation.

## Screenshots

(Include relevant screenshots here)

## Troubleshooting

If you encounter any issues, check the following:

- Ensure all setup steps have been correctly followed.
- Verify all dependencies are installed.
- Review AWS CloudWatch logs for errors.
- Refer to the project rubric for additional guidance and requirements.

## License

This project is licensed under the MIT License.

## Acknowledgements

- **Udacity**: For the Cloud DevOps Engineer Nanodegree program.
- **AWS**: For cloud services and infrastructure.
- **Kubernetes**: For the container orchestration platform.

---
