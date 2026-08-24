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

Recommended screenshots:

1. Docker image
2. Amazon ECR repository
3. EKS cluster
4. Kubernetes pods
5. Kubernetes LoadBalancer
6. AWS CodeBuild
7. AWS CodePipeline showing Source → Build → Deploy
8. CloudWatch log groups
9. Running application

## 18. Final Result

The React application was successfully containerized, stored in Amazon ECR, deployed to Amazon EKS, automated using AWS CodePipeline and CodeBuild, and monitored using Amazon CloudWatch.

Final deployment flow:

GitHub → CodePipeline → CodeBuild → Amazon ECR → EKS Deploy → Amazon EKS → LoadBalancer → React Application
