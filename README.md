# Brain Tasks App – AWS DevOps Deployment

## 1. Project Overview

This project demonstrates the deployment of a React application using AWS DevOps services.

The application is containerized using Docker, stored in Amazon ECR, deployed to Amazon EKS using Kubernetes, automated using AWS CodeBuild and AWS CodePipeline, and monitored using Amazon CloudWatch.

## 2. Architecture

GitHub → AWS CodePipeline → AWS CodeBuild → Amazon ECR → EKS Deploy → Amazon EKS → LoadBalancer → Application

## 3. Technologies Used

- React
- Docker
- Amazon ECR
- Amazon EKS
- Kubernetes
- AWS CodeBuild
- AWS CodePipeline
- Amazon CloudWatch
- GitHub

## 4. Docker

The application was containerized using a Dockerfile.

The Docker image was built and tested before being pushed to Amazon ECR.

Docker image repository:

`858656722878.dkr.ecr.eu-north-1.amazonaws.com/brain-tasks-app`

The application runs on port `3000` inside the container.

## 5. Amazon ECR

Amazon ECR is used as the container image registry.

Repository:

`brain-tasks-app`

Region:

`eu-north-1`

## 6. Amazon EKS

An Amazon EKS cluster was created for application deployment.

Cluster:

`brain-tasks-cluster`

Region:

`eu-north-1`

The cluster was verified to be active.

## 7. Kubernetes Deployment

The application is deployed using `deployment.yaml`.

The Deployment contains:

- Application name: `brain-tasks-app`
- Replicas: `1`
- Container port: `3000`
- Image: Amazon ECR

## 8. Kubernetes Service

The application is exposed using `service.yaml`.

Service:

`brain-tasks-service`

Service type:

`LoadBalancer`

Port configuration:

- Port: `80`
- Target Port: `3000`

## 9. GitHub

Repository:

`https://github.com/AnbanSiddharthan/Brain-Tasks-App-DevOps`

The `main` branch is connected to AWS CodePipeline.

Git CLI was used to commit and push the project.

## 10. AWS CodeBuild

CodeBuild project:

`brain-tasks-build`

Region:

`eu-north-1`

The CodeBuild process:

1. Logs in to Amazon ECR
2. Builds the Docker image
3. Tags the Docker image
4. Pushes the image to Amazon ECR

The build configuration is defined in `buildspec.yml`.

## 11. AWS CodePipeline

Pipeline:

`brain-tasks-pipeline`

The pipeline contains three stages:

**Source → Build → Deploy**

### Source

The source is the GitHub repository:

`AnbanSiddharthan/Brain-Tasks-App-DevOps`

Branch:

`main`

### Build

AWS CodeBuild builds the Docker image and pushes it to Amazon ECR.

### Deploy

The Deploy stage deploys the Kubernetes manifests to Amazon EKS.

Manifests:

- `deployment.yaml`
- `service.yaml`

Target cluster:

`brain-tasks-cluster`

Pipeline execution was successfully verified:

- Source — Succeeded
- Build — Succeeded
- Deploy — Succeeded

## 12. CloudWatch Monitoring

Amazon CloudWatch is used to monitor the application and deployment environment.

The following log groups are available:

- `/aws/codebuild/brain-tasks-build`
- `/aws/codepipeline/brain-tasks-pipeline`
- `/aws/containerinsights/brain-tasks-cluster/application`
- `/aws/containerinsights/brain-tasks-cluster/dataplane`
- `/aws/containerinsights/brain-tasks-cluster/host`
- `/aws/containerinsights/brain-tasks-cluster/performance`

The Amazon CloudWatch Observability add-on is installed in the EKS cluster.

## 13. Application

Application URL:

`http://ae8af0ffae3fa4f5e8c8a31576984c12-1896103079.eu-north-1.elb.amazonaws.com`

## 14. LoadBalancer ARN

`arn:aws:elasticloadbalancing:eu-north-1:858656722878:loadbalancer/ae8af0ffae3fa4f5e8c8a31576984c12`

## 15. Deployment Verification

The following were successfully verified:

- EKS cluster is active
- Application pod is running
- Kubernetes LoadBalancer is available
- Docker image is stored in ECR
- CodeBuild completed successfully
- CodePipeline Source completed successfully
- CodePipeline Build completed successfully
- CodePipeline Deploy completed successfully
- CloudWatch log groups are available
- Application is accessible through the LoadBalancer

## 16. Project Files

- `Dockerfile`
- `buildspec.yml`
- `deployment.yaml`
- `service.yaml`
- `dist/`
- `README.md`

## 17. Screenshots

Screenshots can be added to this README as deployment evidence.


### Docker image

<img width="1906" height="527" alt="image" src="https://github.com/user-attachments/assets/0e8b054f-57d3-417e-b60c-3bd730385f2e" />

### Amazon ECR repository

<img width="1917" height="846" alt="image" src="https://github.com/user-attachments/assets/f0d8013d-9179-4475-ab65-334b89230efd" />

### EKS cluster

<img width="1916" height="901" alt="image" src="https://github.com/user-attachments/assets/bfb01794-1c92-40b3-9765-17b3ea56fd41" />

### Kubernetes pods

<img width="1902" height="112" alt="image" src="https://github.com/user-attachments/assets/40fa94d1-857b-4443-a23e-6e6cff83d34d" />

### Kubernetes LoadBalancer

<img width="1906" height="115" alt="image" src="https://github.com/user-attachments/assets/d1a81d77-d620-4b2f-b571-bc86df91b48f" />

### AWS CodeBuild

<img width="1917" height="868" alt="image" src="https://github.com/user-attachments/assets/235b7f5d-cf98-4356-a0f8-ea329304d891" />

### AWS CodePipeline showing Source → Build → Deploy

<img width="1917" height="867" alt="image" src="https://github.com/user-attachments/assets/d5a63a14-38ec-4ed0-8896-66540ecc0c9d" />

### CloudWatch log groups

<img width="1917" height="807" alt="image" src="https://github.com/user-attachments/assets/404830b9-e6c2-45dd-905b-9c6989f3dd0d" />

### Running application

<img width="1910" height="973" alt="image" src="https://github.com/user-attachments/assets/20c9d8a7-a25a-45f9-a20e-6be3a7250cc6" />


## 18. Final Result

The React application was successfully containerized, stored in Amazon ECR, deployed to Amazon EKS, automated using AWS CodePipeline and CodeBuild, and monitored using Amazon CloudWatch.

Final deployment flow:

GitHub → CodePipeline → CodeBuild → Amazon ECR → EKS Deploy → Amazon EKS → LoadBalancer → React Application
