# 🚀 ASG-LB-G: Auto Scaling Group with Load Balancer
This repository contains the implementation of a web system deployed on AWS, using auto scaling groups (Auto Scaling Group) and load balancers (Load Balancer), with an automated pipeline for main and qa branches.

## 📖 Project Description.
The project consists of the configuration and deployment of a simple web application (index.html) that displays a welcome message. 

## 🔧 CI/CD Pipeline.
A pipeline has been configured in GitHub Actions to automate the following stages:

### 1. 🏗️ Build and Push of Docker Images.
**Source code checkout:** The code is checked out from the repository.
**Docker image build:** An image is generated based on the current code.
**Publishing to the container registry:** The Docker image is published to ghcr.io.

### 2. 📤 Deployment to QA Environment.
When a push is made to the qa branch, it is automatically deployed to two QA instances:
**🔄 Docker image pull:** the latest version of the image is downloaded from the registry.
**🛠️ Instance configuration:** Stops and removes any running containers, and deploys the new image.

### 3. 🌐 Deployment in Production.
When a push is performed to the main branch:
🖼️ The most recent Docker image becomes available for use by the Auto Scaling Group, ensuring that all active instances have the most recent version.

### 🗂️ File Structure
- **index.html:** Static web page with a basic layout and a welcome message.
- **.github/workflows:** CI/CD pipeline configuration for QA and production environments.

### 🌟 Deployment Example.
The application is available through the public DNS of the load balancer. It displays a message like the following:
![image](https://github.com/user-attachments/assets/7fb5c521-cd89-4239-b465-9ced0d58413b)

### ⚙️ Required Configuration
#### 🔑 GitHub secrets.
For the pipeline to work correctly, the following secrets must be configured:
- **GHCR_ACTOR and GHCR_TOKEN:** For authentication with the container registry.
- **QA_INSTANCE_1 and QA_INSTANCE_2:** IP or DNS addresses of the QA instances.
- **EC2_USER and EC2_KEY:** User and SSH key to access the instances.
