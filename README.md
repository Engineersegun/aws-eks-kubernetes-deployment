# aws-eks-kubernetes-deployment
Scalable Kubernetes (EKS) deployment using Docker, Amazon ECR, and AWS Load Balancing.
# AWS Cloud Containerization Project

A hands-on project demonstrating the containerization of a web application using **Docker** and its deployment to **Amazon Elastic Container Registry (ECR)**.

## 🚀 Overview
This project showcases a complete DevOps workflow: taking a local web application, packaging it into a portable Docker image, and pushing it to a secure, cloud-native private registry on AWS.

## 🛠️ Tech Stack
* **Containerization:** Docker
* **Cloud Provider:** Amazon Web Services (AWS)
* **Registry:** Amazon ECR
* **Web Server:** Nginx
* **Environment:** Bash / Terminal

## 🔧 Key Troubleshooting Steps
Every project has its hurdles. During development, I successfully resolved several critical issues:
* **Environment Configuration:** Fixed build-context errors by ensuring the Docker CLI correctly identified the project root.
* **File System Normalization:** Resolved naming conflicts (e.g., hidden `.txt` extensions) that caused Docker build failures.
* **AWS Authentication:** Configured secure CLI access to ECR using IAM credentials and the `get-login-password` protocol.

## 📥 How to Run Locally

1. **Build the image:**
   ```bash
   docker build -t my-app .Run the container:

Bash
2.docker run -d -p 8080:80 my-app

3.View the app: Open localhost:8080 in your browser.

☁️ Deployment to AWS
Authenticate: Run the AWS ECR login command.
Tag: docker tag my-app:latest <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/my-app:latest
Push: docker push <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/my-app:latest
