# Apache Website — DevOps CI/CD Pipeline

Automated deployment of an Apache website using a complete CI/CD pipeline on AWS EC2.

## Pipeline Flow
GitHub → Jenkins → Ansible → Docker → Kubernetes → Live Website

## Tech Stack
- **AWS EC2** — 2 Ubuntu servers (Master + Node)
- **Jenkins** — CI/CD pipeline automation
- **Ansible** — Remote server configuration via SSH
- **Docker** — Container build and push to DockerHub
- **Kubernetes** — 2 pod deployment with NodePort service
- **GitHub** — Source control and Jenkinsfile

## Architecture
- Master node runs Jenkins, Ansible, Kubernetes control plane
- Worker node runs the deployed Apache website pods
- Jenkins pipeline triggers automatically on code push
- Website accessible at node-ip:30080

## Pipeline Stages
1. Checkout SCM — pulls code from GitHub
2. Clone Git repository — clones latest code
3. Run Ansible Playbook — installs Apache on node
4. Docker Build and Push — builds image, pushes to DockerHub
5. Deploy to Kubernetes — applies deployment and service

## How to Run
1. Clone this repository
2. Set up 2 EC2 instances (master and node)
3. Install Jenkins, Docker, Kubernetes, Ansible on master
4. Configure Jenkins credentials for Docker and Ansible
5. Run the Jenkins pipeline

## Project Screenshots
screenshots/pipeline.png
screenshots/pods running.png
screenshots/website.png
screenshots/Ec2.png
screenshots/dockerhub.png

## Author
Akash Pedraj
[LinkedIn](https://www.linkedin.com/in/akash-pedraj/)
[GitHub](https://github.com/AkashPedraj)
