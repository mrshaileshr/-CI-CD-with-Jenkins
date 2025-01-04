# Deployment Process

This README file explains the deployment process for the application, including dependency installation, local build and run, infrastructure planning, Docker image creation, ECR push, Kubernetes deployment, infrastructure provisioning, and notifications.

## Stages

### 1. Install Dependencies
Install the necessary dependencies:
- AWS CLI
- Terraform
- Helm

### 2. Build & Run Locally
Build and run the frontend and backend applications locally within Docker containers:
```sh
docker-compose up --build

terraform init
terraform plan
### 3. Infrastructure Planning
docker build -t <frontend-image-name> ./frontend
docker build -t <backend-image-name> ./backend

### 4. Build Docker Images
docker build -t <frontend-image-name> ./frontend
docker build -t <backend-image-name> ./backend

###5. 5. Push to ECR
aws ecr get-login-password --region <region> | docker login --username AWS --password-stdin <account-id>.dkr.ecr.<region>.amazonaws.com
docker tag <frontend-image-name>:latest <account-id>.dkr.ecr.<region>.amazonaws.com/<frontend-repo>:latest
docker tag <backend-image-name>:latest <account-id>.dkr.ecr.<region>.amazonaws.com/<backend-repo>:latest
docker push <account-id>.dkr.ecr.<region>.amazonaws.com/<frontend-repo>:latest
docker push <account-id>.dkr.ecr.<region>.amazonaws.com/<backend-repo>:latest

### 6. Kubernetes Deployment
helm upgrade --install frontend ./helm/frontend
helm upgrade --install backend ./helm/backend

### 7. Infrastructure Provisioning
terraform apply
