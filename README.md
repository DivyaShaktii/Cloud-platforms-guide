# Cloud-platforms-guide
Documenting steps  - application from local to Cloud

#AWS ECS Deployment

Prerequisites

AWS account with necessary permissions
AWS CLI installed and configured locally
Docker image built and ready
Steps

Create an ECR Repository:

Go to the Amazon Elastic Container Registry (ECR) service in your AWS console.
Click "Create repository" and provide a name.
Push Docker Image to ECR:

Tag your image: 'docker tag your-image:latest aws_account_id.dkr.ecr.region.amazonaws.com/your-repo-name:latest'
Log in to ECR: aws ecr get-login-password --region region | docker login --username AWS --password-stdin aws_account_id.dkr.ecr.region.amazonaws.com
Push the image: docker push aws_account_id.dkr.ecr.region.amazonaws.com/your-repo-name:latest
Create an ECS Cluster:

Go to the Amazon Elastic Container Service (ECS) in your AWS console.
Click "Create Cluster," and choose a suitable networking and compute option (EC2 or Fargate).
Create a Task Definition:

Go to the ECS console and create a new task definition.
Select launch type (EC2 or Fargate), specify your image URI from ECR, memory/CPU, port mappings, and any environment variables.
Create an ECS Service:

In the ECS console, create a service.
Choose your cluster, task definition, the desired number of tasks, and load balancer configuration (if needed).
Access Your Application:

Once the service is running, look for the public IP or load balancer DNS to access your application.
