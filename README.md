# Host-a-Dynamic-Web-App-on-AWS-with-Terraform-Docker-Amazon-ECR-and-ECS


This project demonstrates how to deploy a **dynamic, containerized web application** on AWS using modern DevOps tools and services: **Terraform**, **Docker**, **Amazon Elastic Container Registry (ECR)**, and **Amazon Elastic Container Service (ECS)** with **Fargate**.

---

##  Project Goals

-  Containerize a dynamic web app using Docker  
-  Store and manage images in Amazon ECR  
-  Deploy containers using AWS ECS with Fargate (serverless)  
-  Automate infrastructure provisioning with Terraform  
-  Expose the app securely via Application Load Balancer  

---

##  Tech Stack

| Tool/Service | Role |
|--------------|------|
| **Docker** | Containerizes the web app |
| **Amazon ECR** | Private container image storage |
| **Amazon ECS (Fargate)** | Serverless container orchestration |
| **Terraform** | Infrastructure as Code (IaC) |
| **ALB (Elastic Load Balancer)** | Routes traffic to your service |
| **IAM & Security Groups** | Secure access and roles |
| **CloudWatch** | Logging and monitoring |

---

## Folder Structure

```bash
.
├── app/                  # Your dynamic web application (e.g., Flask, Node.js)
│   └── Dockerfile        # Dockerfile to containerize the app
├── terraform/
│   ├── main.tf           # Main Terraform configuration
│   ├── variables.tf      # Input variables
│   ├── outputs.tf        # Outputs (like ALB DNS name)
│   └── ecs.tf            # ECS and task/service definitions
├── scripts/
│   └── push-to-ecr.sh    # Script to build and push Docker image to ECR
```

---

##  Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/aws-dynamic-webapp-terraform-docker.git
cd aws-dynamic-webapp-terraform-docker
```

### 2. Configure AWS CLI

```bash
aws configure
```

### 3. Build and Push Docker Image to ECR

```bash
cd scripts/
chmod +x push-to-ecr.sh
./push-to-ecr.sh
```

> This script:
> - Creates an ECR repo if it doesn't exist  
> - Builds the Docker image  
> - Tags and pushes it to Amazon ECR

### 4. Deploy Infrastructure with Terraform

```bash
cd terraform/
terraform init
terraform plan
terraform apply
```

> Terraform provisions:
> - VPC, Subnets, Internet Gateway, Security Groups  
> - ECS Cluster, Task Definitions, IAM Roles  
> - Application Load Balancer for public access  

### 5. Set  Domain and Hosted Zone
---
variable "domain_name" {
  default = "mydomain.com"
}

variable "hosted_zone_id" {
  default = "My Route 53 Hosted Zone ID" 
}

##  Security Notes

- IAM roles follow least privilege principles  
- Security groups restrict access to HTTP (port 80)  
- Logging is enabled via CloudWatch  

---

##  Highlights

-  Reusable Terraform templates  
-  Cloud-native deployment on AWS  
-  Dockerized microservice architecture  
-  Push-to-deploy with ECR + ECS  
