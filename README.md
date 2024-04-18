# Coworking Space Service
This project is part of the Udacity Cloud DevOps Engineer Nanodegree program. It involves building and deploying a microservice for a coworking space.

Project Overview
The Coworking Space Service project aims to create a scalable and reliable microservice using Kubernetes and AWS services. The microservice will handle various functionalities related to managing a coworking space, such as user registration, booking management, and resource allocation.

Technologies Used
Docker: Containerization platform used to package the microservice.
AWS ECR: Elastic Container Registry used to store Docker images.
AWS CodeBuild: Continuous integration and deployment service used to build and deploy the Docker image.
Kubernetes: Container orchestration platform used to manage and scale the microservice.
AWS RDS: Relational Database Service used to host the Postgres database.
AWS CloudWatch: Monitoring and logging service used to monitor the application's health and performance.
Project Setup
To set up and run the Coworking Space Service, follow these steps:

Clone the project repository: git clone <repository-url>
Navigate to the project directory: cd coworking-space-service
Build the Docker image: docker build -t coworking-service .
Push the Docker image to AWS ECR: docker push <aws-ecr-repository-url>
Set up the Kubernetes cluster: kubectl apply -f kubernetes/cluster.yaml
Deploy the microservice: kubectl apply -f kubernetes/deployment.yaml
Create the service: kubectl apply -f kubernetes/service.yaml
Set up the database service: kubectl apply -f kubernetes/database.yaml
Usage
To use the Coworking Space Service, follow these steps:

Access the microservice API by using the service's external IP address.
Use the API endpoints to perform various actions, such as user registration, booking management, and resource allocation.
Screenshots
Include relevant screenshots of your project here, such as:

Screenshot of the Docker image pushed to AWS ECR.
Screenshot of the CodeBuild pipeline triggering the build and pushing the Docker image to ECR.
Screenshot of the Kubernetes service created.
Screenshot of the Kubernetes deployment description.
Screenshot of the running pods in the Kubernetes cluster.
Screenshot of the Postgres database service in Kubernetes.
Troubleshooting
If you encounter any issues while setting up or running the Coworking Space Service, try the following:

Double-check that you have followed all the setup steps correctly.
Verify that all the required dependencies are installed.
Check the logs in AWS CloudWatch for any error messages.
Refer to the project rubric for additional guidance and requirements.
License
This project is licensed under the MIT License(opens in a new tab).

Acknowledgements
Udacity for providing the Cloud DevOps Engineer Nanodegree program.
AWS for their cloud services and infrastructure.
Kubernetes for the container orchestration platform.
