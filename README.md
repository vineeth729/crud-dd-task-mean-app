# CRUD MEAN Application Deployment

This repository contains a **MEAN (MongoDB, Express, Angular, Node.js)** CRUD application deployed on an Ubuntu VM using **Docker**, **Docker Compose**, and **Nginx**, with a CI/CD pipeline implemented using Jenkins.

---

## Project Overview

The application includes:

- **Frontend:** Angular  
- **Backend:** Node.js + Express  
- **Database:** MongoDB  
- **Reverse Proxy:** Nginx  
- **CI/CD:** Jenkins + Docker Hub   

---

## Workflow
1. Developer pushes changes to **GitHub repository**.
2. Jenkins pipeline detects changes and triggers:
   - Docker image build for frontend and backend.
   - Push images to **Docker Hub**.
3. Ubuntu VM (EC2 or other cloud VM) pulls latest images.
4. Docker Compose brings up all services on the VM.
5. Nginx serves the frontend and proxies API requests to backend.
6. MongoDB stores application data and is linked to the backend container.

## Repository Setup

1. Download the zip file and create a new repository and make Dockerfile for Backend, Frontend and add docker-compose file, Nginx configuration, Jenkinsfile.

<img width="1858" height="1048" alt="image" src="https://github.com/user-attachments/assets/5bdc1625-3986-415c-aab2-d3b5bb25f627" />

   
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/5d279303-d292-4cc1-b785-9e5580f6bea0" />

3. Docker image build process.
Backend:

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/1505def1-e808-46f2-ab16-1df0b78e54dc" />

Frontend:

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/7585f6b1-76e8-4bfb-996a-6d1453c00f01" />


3. Docker image push process.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/77b10088-49d3-425e-9573-b9faf3c3ceba" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/e8a91ebf-624c-4c88-9ac1-7c159f8a699a" />


4. Deployment on Ubuntu VM on AWS from Jenkins.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/9185abfa-f94e-48c0-98f4-f05956ca0ed3" />

5. Running Containers

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/4c6fb79b-d945-4817-b490-e85a7b9ea1d9" />


6. UI on VM

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/4c514462-f327-4fa5-8b27-2675dd779fcd" />


<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/559c83f3-5526-4be4-991b-aa3748f1c8ea" />

6. CI/CD Pipeline

- Implemented using Jenkins:
- Builds and pushes Docker images to Docker Hub on code push
- Pulls the latest images on the VM
- Restarts containers automatically
- Pipeline stages:
- Checkout code from GitHub
- Build Angular frontend

Build and push Docker images (frontend & backend)

Deploy to EC2 using Docker Compose

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/4e70b379-04c1-49e6-aacf-1f07d1a97c58" />


7. Virtual Machine on AWS

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/27fe5618-0aed-4709-a2a1-0bacf8bc084f" />

