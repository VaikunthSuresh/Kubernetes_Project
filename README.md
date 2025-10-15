# Kubernetes_Project : Spring Application Deployment

Overview
This repository demonstrates the containerization and deployment of a Spring Boot application onto a Kubernetes cluster, using Docker for image creation and various Kubernetes manifest files for orchestration.

The project highlights the full CI/CD pipeline foundation, from source code to a scaled, resilient service running in a multi-container environment.

Architecture and Components
The repository is structured to manage three distinct layers:

Component	Files/Folder	Description
Source Code	Spring-Application/	Contains the Java Spring Boot source code for the microservice.
Containerization	Docker-Project/	Contains the Dockerfile and related files used to build the application image.
Kubernetes Config	.yaml files	Defines the desired state of the application within the cluster (Pods, Deployments, Services, etc.).

Kubernetes Resources Included:
namespace.yaml: Defines a dedicated namespace for the application to ensure resource isolation.

demo-pod.yaml: A basic Pod definition used for initial testing and quick deployment.

demo-deployment.yaml: A Deployment object for managing and scaling the demo application.

spring-deployment.yaml: The primary Deployment manifest for the Spring application, including replica configuration.

spring-service.yaml: Defines a Service (likely ClusterIP or NodePort) to expose the Spring application internally or externally.


 Prerequisites
To deploy and run this project, you will need the following tools installed and configured:

Docker: To build the application image.

Kubernetes Cluster: A running cluster (e.g., Minikube, kind, EKS, GKE, or AKS).

kubectl: The Kubernetes command-line tool.

Deployment Steps
Follow these steps to deploy the Spring Boot application onto your Kubernetes cluster:

Step 1: Clone the Repository
Bash

git clone https://github.com/VaikunthSuresh/Kubernetes_Project.git
cd Kubernetes_Project
Step 2: Build the Docker Image
Navigate to the Docker-Project directory and build your application image.

Bash

cd Docker-Project
# Replace <your-docker-username> with your actual Docker Hub username
docker build -t <your-docker-username>/spring-app:latest .
Step 3: Push the Image (Required for remote clusters)
If you are using a cloud-based Kubernetes cluster (EKS, GKE, etc.), you must push the image to a registry.

Bash

docker push <your-docker-username>/spring-app:latest
Step 4: Deploy Kubernetes Resources
Apply the manifest files in the recommended order:

Bash

# 1. Create a dedicated Namespace
kubectl apply -f namespace.yaml

# 2. Deploy the Spring Application Deployment
kubectl apply -f spring-deployment.yaml

# 3. Create the Service to expose the application
kubectl apply -f spring-service.yaml
Step 5: Verify Deployment
Check the status of your Pods and Service:

Bash

# Check if the Pods are running
kubectl get pods -n <namespace-name>

# Check the Service status
kubectl get svc -n <namespace-name>
🧹 Cleanup
To tear down the deployed resources, you can delete the manifest files:

Bash

kubectl delete -f spring-service.yaml
kubectl delete -f spring-deployment.yaml
kubectl delete -f namespace.yaml
