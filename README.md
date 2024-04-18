# Coworking Space Service

This project is a component of the Udacity Cloud DevOps Engineer Nanodegree program. It focuses on building and deploying a microservice for managing a coworking space.

## Project Overview

The Coworking Space Service project is designed to create a scalable and reliable microservice using Kubernetes and AWS services. The microservice will facilitate various functionalities related to managing a coworking space, such as user registration, booking management, and resource allocation.

## Technologies Used

- **Docker**: Containerization platform used to package the microservice.
- **AWS ECR**: Elastic Container Registry for storing Docker images.
- **AWS CodeBuild**: Continuous integration and deployment service for building and deploying the Docker image.
- **Kubernetes**: Container orchestration platform for managing and scaling the microservice.
- **AWS RDS**: Relational Database Service for hosting the Postgres database.
- **AWS CloudWatch**: Monitoring and logging service for tracking the application's health and performance.

## Project Setup

To set up and run the Coworking Space Service, follow these steps:

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
5. Set up the Kubernetes cluster:
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

To utilize the Coworking Space Service, proceed as follows:

1. Access the microservice API using the service's external IP address.
2. Employ the API endpoints for various actions like user registration, booking management, and resource allocation.

## Screenshots

Include relevant screenshots of your project here, such as:

- Screenshot of the Docker image pushed to AWS ECR.
- Screenshot of the CodeBuild pipeline triggering the build and pushing the Docker image to ECR.
- Screenshot of the Kubernetes service created.
- Screenshot of the Kubernetes deployment description.
- Screenshot of the running pods in the Kubernetes cluster.
- Screenshot of the Postgres database service in Kubernetes.

## Troubleshooting

If you encounter any issues while setting up or running the Coworking Space Service, consider the following tips:

- Double-check that you have followed all the setup steps correctly.
- Verify that all required dependencies are installed.
- Check the logs in AWS CloudWatch for any error messages.
- Refer to the project rubric for additional guidance and requirements.

## License

This project is licensed under the MIT License.

## Acknowledgements

- **Udacity**: For offering the Cloud DevOps Engineer Nanodegree program.
- **AWS**: For their cloud services and infrastructure.
- **Kubernetes**: For providing the container orchestration platform.

---
