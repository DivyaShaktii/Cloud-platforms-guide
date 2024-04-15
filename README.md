# Cloud-Platforms-Guide: Documenting Steps - App / Projects from Local to Cloud

## AWS ECS Deployment

**Prerequisites**
  * AWS account with necessary permissions
  * AWS CLI installed and configured locally
  * Docker image built and ready

**Steps**

1. **Create an ECR Repository:**
     * Go to the Amazon Elastic Container Registry (ECR) service in AWS console.
     * Click "Create repository" and provide a name.

2. **Push Docker Image to ECR:**
   Use below commands
     * Tag your image: ```docker tag your-image:latest aws_account_id.dkr.ecr.region.amazonaws.com/your-repo-name:latest```
     * Log in to ECR : ```aws ecr get-login-password --region region | docker login --username AWS --password-stdin aws_account_id.dkr.ecr.region.amazonaws.com ```
     * Push the image : ```docker push aws_account_id.dkr.ecr.region.amazonaws.com/your-repo-name:latest```

3. **Create an ECS Cluster:**
    * Go to the Amazon Elastic Container Service (ECS) in AWS console.
    * Click "Create Cluster," and choose a suitable networking and compute option (EC2 or Fargate).

4. **Create a Task Definition:**
    * Go to the ECS console and create a new task definition.
    * Select launch type (EC2 or Fargate), specify your image URI from ECR, memory/CPU, port mappings, and any environment variables.
      
5. **Create an ECS Service:**
    * In the ECS console, create a service.
    * Choose cluster, task definition, the desired number of tasks, and load balancer configuration (if needed).

6. **Access Your Application:**
    * Once the service is running, look for the public IP or load balancer DNS to access your application.

#
## Google Cloud Deployment (Cloud Run)
Google Cloud Run is the ideal service for Docker-based app deployments.

**Prerequisites**
  * Google Cloud project with billing enabled
  * Google Cloud SDK installed and configured locally
  * Docker image built
    
**Steps:**

1. **Push Image to Google Container Registry (GCR):**
   * Tag your image: ```docker tag your-image:latest gcr.io/your-project-id/your-image-name:latest```
   * Push the image: ```gcloud docker -- push gcr.io/your-project-id/your-image-name:latest```
    
2. **Deploy to Cloud Run:**
   * Create a new Cloud Run service: ```gcloud run deploy --image gcr.io/your-project-id/your-image-name:latest --platform managed```
   * Choose a region, service name, and whether to allow unauthenticated access.
    
3. **Access Your Application:**
    * Cloud Run will provide a service URL to access your application.

#
## Azure Container Instances (ACI) :

**Prerequisites**

  * Azure account with valid subscription
  * Azure CLI installed and configured locally
  * Docker image built and ready
    
**Steps**

  1. **Create an Azure Container Registry (ACR):**
     * In the Azure portal, search for "Container registries" and click "Create".
     * Provide a registry name, resource group, location, and SKU.
  
  2. **Push Image to ACR:**
     * Tag your image: ```docker tag your-image:latest your-acr-name.azurecr.io/your-repo-name:latest```
     * Log in to ACR: ```az acr login --name your-acr-name```
     * Push the image: ```docker push your-acr-name.azurecr.io/your-repo-name:latest```
    
  3. **Create an Azure Container Instance**
     * Using the Azure CLI:
```az container create --resource-group your-resource-group --name your-aci-name --image your-acr-name.azurecr.io/your-repo-name:latest --ports 80 --ip-address ``` (Adjust ports and other settings)

  4. **Using the Azure portal:**
     * Search for "Container Instances" and click "Create".
     * Fill in the resource group, container name, image source (ACR), image, OS type, ports, and other settings.

  5. **Access Your Application**
     * Once the container instance is running, find its public IP address to access your application.




