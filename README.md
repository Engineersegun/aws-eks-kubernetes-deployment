AWS EKS Kubernetes Deployment
<img width="1366" height="768" alt="Screenshot (176)" src="https://github.com/user-attachments/assets/338c31eb-53ab-4817-b5d3-fed8e5edddb9" />
<img width="1024" height="1024" alt="_Generated_Image_vdkq8fvdkq<img width="1024" height="1024" alt="Gemini_Generated_Image_vdkq8fvdkq8fvdkq" src="https://github.com/user-attachments/assets/06fddb1b-d5b8-4046-af54-f103c43bee06" />
8fvdkq" src="https://gi<img width="1366" height="768" alt="Screenshot (195)" src="https://github.com/user-attachments/assets/5464f463-d4a5-4b16-a7fe-24c0cb346321" /> 


thub.com/user-attachments/assets/f8d4470b-0655-4f5f-acb3-1bfd80808989" />

Architected a high-availability EKS cluster with automated scaling and AWS Load Balancer integration.
This project demonstrates a production-grade cloud-native deployment. It covers the full lifecycle of an application—from local containerization with Docker to automated orchestration on Amazon EKS, leveraging Amazon ECR for secure image management and Elastic Load Balancing (ELB) for public traffic distribution.


🚀 Key Features
Managed Infrastructure: Automated cluster provisioning using eksctl for reliable, repeatable environments.
High Availability: Deployed a 2-node managed node group across multiple Availability Zones to ensure fault tolerance.
Container Lifecycle: Implemented a standardized Build-Tag-Push workflow with Docker and Amazon ECR.
Traffic Management: Automatically provisioned an AWS Network Load Balancer via Kubernetes Service manifests.
Scalable Orchestration: Utilized Kubernetes Deployments to manage redundant pod replicas and self-healing workloads.


🛠 Tech Stack
Cloud Provider: Amazon Web Services (AWS)
Orchestration: Amazon EKS (Elastic Kubernetes Service)
Containerization: Docker
Registry: Amazon ECR (Elastic Container Registry)
Ingress: AWS Elastic Load Balancer (ELB)
CI/CD Tools: AWS CLI, kubectl, eksctl



📂 Project Structure
Plaintext
.
├── app/
│   ├── index.html       # Web application source
│   └── Dockerfile       # Optimized container build instructions
├── k8s-manifests/
│   ├── deployment.yaml  # K8s Deployment (Replicas, ECR Image URI)
│   └── service.yaml     # K8s Service (Type: LoadBalancer)
└── README.md            # Project documentation



⚙️ Getting Started
Prerequisites
AWS CLI configured with administrative permissions.
kubectl and eksctl binaries installed.
Docker Desktop running locally.



1. Provision the Cluster
Provision a managed EKS cluster with a single command:

Bash
eksctl create cluster --name my-eks-cluster --region us-east-1 --nodegroup-name my-nodes --node-type t3.medium --nodes 2 --managed
2. Containerization & Registry Push
Build the image locally and push to your private ECR repository:

Bash
# Build & Tag
docker build -t my-app ./app

# Authenticate Docker to AWS ECR
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com

# Push
docker tag my-app:latest <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/my-app:latest
docker push <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/my-app:latest
3. Kubernetes Deployment
Apply the manifests to the cluster:

Bash
kubectl apply -f k8s-manifests/deployment.yaml
kubectl apply -f k8s-manifests/service.yaml
📊 Verification & Troubleshooting
Verify Deployment Status:


Bash
kubectl get pods -o wide
kubectl get svc my-app-service
Access the application via the EXTERNAL-IP address provided by the Load Balancer.


Key Troubleshooting Resolved:
Registry Auth: Resolved ImagePullBackOff by configuring IAM ECR permissions and the get-login-password protocol.
Networking: Successfully mapped container ports (80) to Load Balancer targets for external accessibility.

🧹 Cleanup
To avoid ongoing AWS charges, decommission all resources:

Bash
kubectl delete service my-app-service
eksctl delete cluster --name my-eks-cluster --region us-east-1
