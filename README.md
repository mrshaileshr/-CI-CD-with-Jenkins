# -CI-CD-with-Jenkins
Stages

The pipeline consists of several stages that are executed sequentially:

Install AWS CLI, Terraform, and Helm:

This stage installs the necessary tools required for interacting with AWS, provisioning infrastructure, and deploying applications with Helm.
Run App on Docker (Frontend & Backend):

This stage builds the frontend and backend applications within Docker containers. It assumes the code for both applications resides in the frontend and backend directories respectively.
Terraform Plan:

This stage initializes the Terraform configuration and executes a plan to preview the infrastructure changes that will be applied.
Build Docker Image (Frontend & Backend):

This stage builds Docker images for the frontend and backend applications. The images are tagged with the latest tag and stored locally.
Push Image to ECR (Frontend & Backend):

This stage assumes an Amazon Elastic Container Registry (ECR) has been configured. It authenticates with ECR using AWS credentials and pushes the built Docker images to the specified ECR repository.
Deploy to Kubernetes (Frontend & Backend):

This stage assumes an EKS cluster named my-cluster exists. It updates the kubeconfig file to point to the EKS cluster and leverages Helm to deploy the frontend and backend applications. Helm charts are assumed to reside in the helm/frontend and helm/backend directories respectively.
Apply Terraform Changes:

This stage applies the infrastructure changes planned in the previous Terraform Plan stage.
Post-processing:

The pipeline sends notifications to a Slack channel (#builds) based on the overall success or failure of the pipeline execution.
