# 🚀 Apache Website — Full DevOps CI/CD Pipeline on AWS

![AWS](https://img.shields.io/badge/AWS-EC2-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white)
![Jenkins](https://img.shields.io/badge/Jenkins-CI%2FCD-D24939?style=for-the-badge&logo=jenkins&logoColor=white)
![Ansible](https://img.shields.io/badge/Ansible-Automation-EE0000?style=for-the-badge&logo=ansible&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Container-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-Orchestration-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-Source%20Control-181717?style=for-the-badge&logo=github&logoColor=white)

> A fully automated CI/CD pipeline that takes code from GitHub and deploys it as a live website on Kubernetes — with zero manual steps.

---

## 📌 Project Overview

This project demonstrates a **production-style DevOps pipeline** built on AWS EC2. Every commit to GitHub automatically triggers Jenkins, which runs Ansible for server configuration, builds and pushes a Docker image, and deploys it to a Kubernetes cluster.

---

## ⚡ Pipeline Flow

```
Code Push to GitHub
        ↓
Jenkins Auto Triggers
        ↓
Ansible Configures Node Server
        ↓
Docker Builds & Pushes Image to DockerHub
        ↓
Kubernetes Deploys 2 Pods
        ↓
Website Live at <node-ip>:30080
```

---

## 🏗️ Architecture

```
┌─────────────────────────────────┐
│         Master EC2              │
│  ┌─────────┐  ┌──────────────┐  │
│  │ Jenkins │  │    Ansible   │  │
│  └─────────┘  └──────────────┘  │
│  ┌─────────┐  ┌──────────────┐  │
│  │ Docker  │  │  K8s Master  │  │
│  └─────────┘  └──────────────┘  │
└─────────────────────────────────┘
                ↓
┌─────────────────────────────────┐
│          Node EC2               │
│  ┌──────────────────────────┐   │
│  │  Kubernetes Worker Node  │   │
│  │  Apache Pod 1            │   │
│  │  Apache Pod 2            │   │
│  └──────────────────────────┘   │
└─────────────────────────────────┘
```

---

## 🛠️ Tech Stack

| Tool | Version | Purpose |
|------|---------|---------|
| AWS EC2 | Ubuntu 24.04 | 2 cloud servers — Master and Node |
| Jenkins | 2.x | CI/CD pipeline automation |
| Ansible | Latest | Remote server configuration via SSH |
| Docker | Latest | Container build and push |
| Kubernetes | 1.29 | Container orchestration — 2 pod deployment |
| DockerHub | — | Container image registry |
| GitHub | — | Source control and Jenkinsfile |

---

## 📋 Pipeline Stages

| # | Stage | What Happens |
|---|-------|-------------|
| 1 | Checkout SCM | Jenkins pulls Jenkinsfile from GitHub |
| 2 | Clone Repository | Latest application code is cloned |
| 3 | Ansible Playbook | Apache installed and started on node |
| 4 | Docker Build and Push | Image built and pushed to DockerHub |
| 5 | Deploy to Kubernetes | Deployment and Service applied to cluster |

---

## 📸 Screenshots

| Screenshot | Link |
|------------|------|
| Jenkins Pipeline — All Stages Passed | [View](screenshots/pipeline.png) |
| Kubernetes Pods Running | [View](screenshots/pods%20running.png) |
| Live Website | [View](screenshots/website.png) |
| AWS EC2 Instances | [View](screenshots/Ec2.png) |
| DockerHub Image Pushed | [View](screenshots/dockerhub.png) |

## 🚀 How to Run

```bash
# 1. Fork and clone this repository
git clone https://github.com/AkashPedraj/apachewebsite.git
cd apachewebsite

# 2. Launch 2 EC2 instances on AWS (Ubuntu 24.04)
#    Name them: master and node

# 3. On master — run these installs
#    Docker, Jenkins, Kubernetes, Ansible

# 4. Update inventory.ini with your node private IP
#    [ansiblegroup]
#    <node-private-ip> ansible_user=devops

# 5. Add Jenkins credentials
#    docker      — DockerHub username and password
#    ansible-ssh — SSH private key of devops user
#    kubeconfig  — Kubernetes config secret file

# 6. Create pipeline job in Jenkins
#    Point to this repo → Run Build Now
```

---

## 📁 Repository Structure

```
apachewebsite/
├── Dockerfile          # Docker image build instructions
├── Jenkinsfile         # CI/CD pipeline definition
├── deployment.yml      # Kubernetes deployment manifest
├── service.yml         # Kubernetes NodePort service
├── installapche.yml    # Ansible playbook for Apache
├── inventory.ini       # Ansible inventory file
└── screenshots/        # Project screenshots
```

---

## 💡 Key Learnings

- Building a Kubernetes cluster from scratch using kubeadm on bare EC2
- Writing Jenkins declarative pipelines with full SCM integration
- Ansible SSH key-based authentication across remote servers
- Docker image build, tag and push to DockerHub automation
- Kubernetes Deployments, Services and NodePort configuration
- Debugging real-world SSH permission and connectivity issues across tools

---

## 👨‍💻 Author

**Akash Pedraj**

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Akash%20Pedraj-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/akash-pedraj/)
[![GitHub](https://img.shields.io/badge/GitHub-AkashPedraj-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/AkashPedraj)

---

⭐ If this project helped you, please give it a star!
