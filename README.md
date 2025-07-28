# 🚀 Dockerized Application Deployment on AWS EC2

![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=for-the-badge&logo=amazon-aws&logoColor=white)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)

This repository documents the process of deploying a Dockerized web application from Docker Hub to a live cloud server on an **Amazon Web Services (AWS) EC2 instance**.

---

### 🎯 Project Goal

The objective of this project was to take a pre-existing Docker image of a portfolio website and deploy it in a real-world cloud environment. This demonstrates the end-to-end workflow of a modern DevOps deployment.

The live application is accessible at: `http://<Your-Public-IP>:8080`

---

### 📝 Process Overview

Here are the key steps that were followed to achieve the deployment:

**1. Launching an EC2 Instance:**
* An AWS Free Tier account was used.
* A `t3.micro` EC2 instance was launched with the **Ubuntu Server 24.04 LTS** AMI.
* A new Key Pair (`.pem` file) was created for secure SSH access.

**2. Configuring the Firewall (Security Groups):**
* A security group was configured to allow inbound traffic on the following ports:
  * **Port 22 (SSH):** To allow secure remote login to the server.
  * **Port 80 (HTTP):** For standard web traffic.
  * **Port 8080 (Custom TCP):** To allow access to our Docker container.

**3. Setting up the Server Environment:**
* Connected to the EC2 instance via SSH using the downloaded `.pem` key.
* Updated the server's package manager with `sudo apt update`.
* Installed the Docker engine on the Ubuntu server using `sudo apt install docker.io`.
* Added the `ubuntu` user to the `docker` group to run Docker commands without `sudo`.

**4. Deploying the Container:**
* Pulled the portfolio's Docker image from a public Docker Hub repository using `docker pull kunal102/portfolio:latest`.
* Ran the Docker image as a container on the server using the following command:
  ```bash
  docker run -d -p 8080:80 --restart always kunal102/portfolio:latest
