### 🚀 AWS Services Capstone Project — CI/CD Pipeline with Jenkins, Docker & AWS EC2

Production-style DevOps project demonstrating automated CI/CD workflows, Docker container deployment, AWS EC2 integration, and real-world debugging scenarios using Jenkins pipelines.

#### 📌 Project Overview

This capstone project demonstrates a complete CI/CD workflow that automates:

- Application build & packaging
- Docker image creation
- Jenkins multibranch pipelines
- Automated deployment to AWS EC2
- Docker container lifecycle management
- Remote deployment over SSH
- Real-world troubleshooting & recovery

The project extends the DevOps Bootcamp AWS Services module into a more production-oriented implementation by focusing heavily on:

* Infrastructure troubleshooting
* Pipeline reliability
* Docker image management
* Git branch recovery
* Jenkins debugging
* Deployment consistency

Unlike tutorial-only implementations, this project includes actual operational failures encountered during development and the fixes applied to stabilize the pipeline.

#### 🏗️ Architecture

```text
GitHub
   ↓
Webhook Trigger
   ↓
Jenkins Multibranch Pipeline
   ↓
Maven Build
   ↓
Docker Build & Tag
   ↓
Docker Hub Registry
   ↓
SSH Deployment to AWS EC2
   ↓
Running Docker Container
```

#### ⚙️ Tech Stack

| Area             | Technologies      |
| ---------------- | ----------------- |
| CI/CD            | Jenkins           |
| Cloud            | AWS EC2           |
| Build Tool       | Apache Maven      |
| Containerization | Docker            |
| SCM              | Git & GitHub      |
| Language         | Java              |
| Pipeline         | Jenkinsfile       |
| Remote Access    | SSH               |
| OS               | Amazon Linux 2023 |
| IDE              | VS Code           |

#### ☁️ AWS Services Used

| AWS Service     | Purpose                 |
| --------------- | ----------------------- |
| Amazon EC2      | Application hosting     |
| Security Groups | Port access control     |
| IAM             | Access & authentication |
| SSH Key Pairs   | Secure remote access    |

#### 📂 Repository Structure

```bash
aws-devops-pipeline/
│
├── Jenkinsfile
├── pom.xml
├── Dockerfile
├── .gitignore
├── src/
├── README.md
└── assets/
```

#### 🔄 CI/CD Pipeline Workflow

#### 1️⃣ Source Code Management

* GitHub repository connected to Jenkins Multibranch Pipeline
* Feature branches automatically discovered
* Webhook triggers automated builds on push events

Example branches:

```bash
feature/payment
jenkins-jobs
master
starting-code
```

#### 2️⃣ Build Stage

The application is compiled using Maven.

Pipeline performs:

* Dependency resolution
* Application packaging
* Artifact generation
* Test execution

The Maven project configuration includes Spring Boot and compiler configuration. 

#### 3️⃣ Docker Build Stage

Docker images are built automatically during the pipeline.

Example:

```bash
docker build -t miguelprint/my-app:1.0 .
```

This produced a successfully built Docker image locally before deployment.

#### 4️⃣ Docker Registry Integration

Images are tagged and pushed to Docker Hub for deployment consistency.

Example image tags used:

```bash
miguelprint/demo-app:java-maven-1.0
miguelprint/demo-app:java-maven-2.0
```

<img src="assets/one of the images pushed.png" width="600">

#### 5️⃣ AWS EC2 Deployment

The Jenkins pipeline deploys containers remotely to an EC2 instance using SSH credentials.

Deployment tasks included:

* Connecting via SSH
* Pulling Docker images
* Running containers
* Mapping exposed ports
* Managing running containers

Example EC2 host:

```bash
ec2-user@3.8.155.161
```

<img src="assets/running images and containers of ec2-user@3.8.155.161.png" width="600">

#### 🧪 Real-World Challenges & Debugging

One of the strongest parts of this project was the amount of production-style troubleshooting involved.

This project was not just about “following tutorials” — it required diagnosing actual CI/CD failures and infrastructure issues.

#### ❌ Challenge 1 — Git Upstream Tracking Misconfiguration

#### Problem

After cloning the repository, branches were incorrectly tracking `upstream` instead of `origin`.

<img src="assets/9 - after cloning, tracking upstream instead of origin.png" width="600">

This caused:

* Branch confusion
* Incorrect pull/push targets
* Merge inconsistencies
* Jenkins pipeline instability

#### Example Symptoms

```bash
upstream/jenkins-jobs
origin/jenkins-jobs
```

#### Resolution

Used Git recovery techniques including:

```bash
git reflog --oneline
git reset --hard
git push --force-with-lease
```

This restored the correct repository state and stabilized the multibranch pipeline.

#### ❌ Challenge 2 — Docker Image Conflicts

#### Problem

Multiple Docker images and stopped containers created conflicts during deployments.

<img src="assets/container images mixed up.png" width="600">

Errors encountered:

```bash
image is being used by stopped container
```

This caused:

* Deployment failures
* Disk usage growth
* Environment inconsistency

#### Resolution

Performed container cleanup and image management:

```bash
docker rm <container-id>
docker rmi -f <image-id>
docker ps -a
docker images
```

This restored deployment consistency on the EC2 host.

#### ❌ Challenge 3 — Port Allocation Failures

#### Problem

Deployment attempts failed because ports were already allocated by existing containers.

Example issue:

```bash
Bind for 0.0.0.0:3080 failed: port is already allocated
```

#### Resolution

* Identified running containers
* Removed stale containers
* Restarted deployment with corrected port mapping

#### ❌ Challenge 4 — Jenkins Deployment Failures

#### Problem

Initial pipeline deployments failed during the deploy stage.

Issues included:

* Incorrect Docker image references
* SSH deployment problems
* Remote container conflicts
* Branch tracking problems

#### Resolution

The Jenkins pipeline was corrected and rebuilt successfully.

Final pipeline stages:

* Checkout SCM
* Test
* Build
* Deploy

All stages completed successfully in the final pipeline execution.

<img src="assets/Build ok after fixing upstream.png" width="600">

#### 🔐 Jenkins Credentials & Security

The pipeline used Jenkins Credentials Management for secure authentication.

Credentials configured included:

* Docker Hub credentials
* EC2 SSH private key
* Git authentication

This avoided hardcoding sensitive credentials into the pipeline.

#### 📦 Docker Container Management

During deployment, several operational tasks were performed:

#### Running Containers

```bash
docker ps
```

#### Remove Stopped Containers

```bash
docker rm <container-id>
```

#### Remove Images

```bash
docker rmi -f <image-id>
```

#### Verify Running Services

```bash
docker images
docker ps -a
```

#### ☁️ AWS Infrastructure Setup

#### EC2 Configuration

* Amazon Linux 2023
* Docker installed manually
* Security groups configured
* Port 8080 exposed
* SSH access configured via PEM key

#### 📈 DevOps Concepts Demonstrated

This project demonstrates practical implementation of:

* CI/CD Automation
* Pipeline as Code
* Multibranch Jenkins Pipelines
* Docker Containerization
* AWS EC2 Deployments
* Git Branch Recovery
* Remote Deployment Automation
* Infrastructure Troubleshooting
* Build Automation
* Container Lifecycle Management

#### 🔮 Future Improvements

Planned next steps:

* Deploy images to AWS ECR
* Kubernetes deployment with EKS
* Infrastructure as Code with Terraform
* Jenkins Shared Libraries
* Monitoring with Prometheus & Grafana
* Automated rollback strategies
* Blue/Green deployments

**Author:** Miguel (DevOps Engineer)

Focused on building production-oriented DevOps projects with real operational troubleshooting experience, cloud infrastructure integration, and CI/CD automation.

**Learning Source:** TechWorld with Nana DevOps Bootcamp

This implementation significantly extends the original exercises through additional debugging, deployment recovery, infrastructure troubleshooting, and production-style operational practices.

#### 📎 Supporting Project Files

* Jenkins pipeline configuration included in uploaded project files
* Maven project configuration included in `pom.xml` 
* Git ignore configuration included in `.gitignore` 
* Previous CI/CD project structure reference provided in uploaded markdown 
