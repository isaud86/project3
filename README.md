
## Coworking Space Service

This project involves deploying an analytics application using Docker, AWS services, and Kubernetes. The process includes setting up a PostgreSQL database, creating a Docker image of the application, and deploying it to a Kubernetes cluster managed by Amazon EKS.

## Getting Started

### Initial Setup

1. **Fork and Clone the Repository**
   - Fork the starter project to your GitHub account.
   - Clone your forked repository:
     ```bash
     git clone <repository-url>
     ```
   - Generate an SSH key and add it to your GitHub account to secure connections:
     ```bash
     ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
     ```

### Configure Your Environment

2. **Install Necessary Tools**
   - **Git**: For version control.
     ```bash
     sudo apt-get install git
     ```
   - **Docker CLI**: To build and run Docker images locally.
     ```bash
     sudo apt-get install docker.io
     ```
   - **kubectl**: For interacting with Kubernetes clusters.
     ```bash
     sudo snap install kubectl --classic
     ```
   - **AWS CLI v2**: For interacting with AWS services.
     ```bash
     curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
     unzip awscliv2.zip
     sudo ./aws/install
     ```

3. **AWS Configuration**
   - Configure AWS CLI:
     ```bash
     aws configure
     ```
   - Verify installation and configuration:
     ```bash
     aws sts get-caller-identity
     ```

### Create and Manage Kubernetes Cluster

4. **EKS Cluster Setup**
   - Use `eksctl` to create the EKS cluster:
     ```bash
     eksctl create cluster --name my-cluster --region us-east-1 --nodegroup-name my-nodes --node-type t3.small --nodes 1 --nodes-min 1 --nodes-max 2
     ```
   - Update your Kubeconfig to interact with the new cluster:
     ```bash
     aws eks --region us-east-1 update-kubeconfig --name my-cluster
     ```

### Database Configuration

5. **Set Up PostgreSQL in Kubernetes**
   - Apply PersistentVolumeClaim:
     ```bash
     kubectl apply -f pvc.yaml
     ```
```bash
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: postgresql-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
```
   - Apply PersistentVolume:
     ```bash
     kubectl apply -f pv.yaml
     ```
     ```bash
     apiVersion: v1
      kind: PersistentVolume
      metadata:
        name: my-manual-pv
      spec:
        capacity:
          storage: 1Gi
        accessModes:
          - ReadWriteOnce
        persistentVolumeReclaimPolicy: Retain
        storageClassName: gp2
        hostPath:
          path: "/mnt/data"
    ```
   - Deploy PostgreSQL using a Deployment configuration:
     ```bash
     kubectl apply -f postgresql-deployment.yaml
     ```
     ```bash
           apiVersion: apps/v1
         kind: Deployment
      metadata:
        name: postgresql
      spec:
        selector:
          matchLabels:
            app: postgresql
        template:
          metadata:
            labels:
              app: postgresql
          spec:
            containers:
            - name: postgresql
              image: postgres:latest
              env:
              - name: POSTGRES_DB
                value: mydatabase
              - name: POSTGRES_USER
                value: myuser
              - name: POSTGRES_PASSWORD
                value: mypassword
              ports:
              - containerPort: 5432
              volumeMounts:
              - mountPath: /var/lib/postgresql/data
                name: postgresql-storage
            volumes:
            - name: postgresql-storage
              persistentVolumeClaim:
                claimName: postgresql-pvc
      ```

### Application Deployment

6. **Build and Deploy the Application**
   - Dockerize the application:
     ```bash
     docker build -t my-analytics-application .
     ```
   - Push the Docker image to AWS ECR:
     ```bash
     aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <aws_account_id>.dkr.ecr.us-east-1.amazonaws.com
     docker tag my-analytics-application:latest <aws_account_id>.dkr.ecr.us-east-1.amazonaws.com/my-analytics-application:latest
     docker push <aws_account_id>.dkr.ecr.us-east-1.amazonaws.com/my-analytics-application:latest
     ```
   - Deploy the application using Kubernetes:
     ```bash
     kubectl apply -f deployment.yaml
     kubectl apply -f service.yaml
     ```

### Monitoring and Logging

7. **Set Up CloudWatch Logging**
   - Configure CloudWatch for Kubernetes logging:
     ```bash
     kubectl apply -f cloudwatch-insights.yaml
     ```

## Usage

After deployment, access the application through the exposed Kubernetes service endpoint:
- Retrieve service details:
  ```bash
  kubectl get svc
  ```

## Troubleshooting

For any issues:
- Check pod status:
  ```bash
  kubectl get pods
  ```
- Describe pods to diagnose issues:
  ```bash
  kubectl describe pod <pod_name>
  ```

## Continuous Improvement

- Update Docker images and Kubernetes configurations to accommodate application changes.
- Use AWS CloudWatch to monitor application performance and logs.

## Acknowledgments

- Thanks to Udacity for the educational platform and resources.
- AWS for providing the cloud services essential for this project.
- Kubernetes community for support and resources.
