# CONTAINERIZATION AND DEVOPS LAB

## Experiment 7:  
### CI/CD using Jenkins, GitHub and Docker Hub

**Reference Link:**  
https://upessocs.github.io/#dir=/Lectures/Containerization%20and%20DevOps/Lab/&file=Experiment%2007%20CICD%20using%20Jenkins,%20GitHub%20and%20Docker%20Hub.md

---

## 1. Aim

To design and implement a complete CI/CD pipeline using Jenkins, integrating source code from GitHub, and building & pushing Docker images to Docker Hub.

---

## 2. Objectives

- Understand CI/CD workflow using Jenkins (GUI-based tool)
- Create a structured GitHub repository with application + Jenkinsfile
- Build Docker images from source code
- Securely store Docker Hub credentials in Jenkins
- Automate build & push process using webhook triggers
- Use same host (Docker) as Jenkins agent

---

## 3. Theory

### What is Jenkins?

Jenkins is a web-based GUI automation server used to:

- Build applications  
- Test code  
- Deploy software  

It provides:

- Dashboard (browser-based UI)  
- Plugin ecosystem (GitHub, Docker, etc.)  
- Pipeline as Code using `Jenkinsfile`  

---

### What is CI/CD?

- **Continuous Integration (CI):**  
  Code is automatically built and tested after each commit  

- **Continuous Deployment (CD):**  
  Built artifacts (Docker images) are automatically delivered/deployed  

---

## 4. Prerequisites

- Docker & Docker Compose installed  
- GitHub account  
- Docker Hub account  
- Basic Linux command knowledge

---

# Part A: GitHub Repository Setup (Source Code + Build Definition)

### 1. Create Repository  
A GitHub repository named **my-app** was created to store the project files.  
  
![Image](Images/Images%20Exp7/1.png)  

### 2. Project Structure  
The repository contains the following files:
- Dockerfile  
- Jenkinsfile  
- app.py  
- requirements.txt  
- README.md

![Image](Images/Images%20Exp7/2.png)  

![Image](Images/Images%20Exp7/3.png)  

### 3. Application Code  
A simple Python application was created using Flask framework.  

![Image](Images/Images%20Exp7/4.png)  

![Image](Images/Images%20Exp7/5.png)  

### 4. Dockerfile (Build Process)  
A Dockerfile was created to containerize the application and define the build steps.  

![Image](Images/Images%20Exp7/6.png)  

### 5. Jenkinsfile (Pipeline Definition in GitHub)  
A Jenkinsfile was added to define the CI/CD pipeline including:
- Cloning repository  
- Building Docker image  
- Logging into Docker Hub  
- Pushing Docker image

![Image](Images/Images%20Exp7/7.png)  

---

# Part B: Jenkins Setup using Docker (Persistent Configuration)

### 1. Create Docker Compose file  
A Docker Compose file was used to run Jenkins container with persistent storage.  

![Image](Images/Images%20Exp7/8.png)  

### 2. Run Jenkins  
Jenkins was started using Docker and accessed via:  
http://localhost:8080  

![Image](Images/Images%20Exp7/9.png)  

### 3. Unlock Jenkins  
Jenkins was unlocked using the initial admin password from the container.  

![Image](Images/Images%20Exp7/10.png)  

![Image](Images/Images%20Exp7/11.png)  

![Image](Images/Images%20Exp7/12.png)  

![Image](Images/Images%20Exp7/13.png)  

![Image](Images/Images%20Exp7/14.png)  

---

# Part C: Jenkins Configuration

### 1. Add Docker Hub Credentials  
Docker Hub access token was generated and added to Jenkins credentials securely.  

![Image](Images/Images%20Exp7/15.png)  

![Image](Images/Images%20Exp7/16.png)  

### 2. Create Pipeline Job  
A pipeline job named **ci-cd-pipeline** was created and configured using the Jenkinsfile.  

![Image](Images/Images%20Exp7/17.png)  

---

# Part D: Build Jenkins

### 1. Build  
The pipeline was executed successfully, performing the following steps:
- Cloned code from GitHub  
- Built Docker image  
- Logged into Docker Hub  
- Pushed image to Docker Hub

![Image](Images/Images%20Exp7/18.png)  

### 2. Result (DockerHub Screenshot)

![Image](Images/Images%20Exp7/19.png)  

![Image](Images/Images%20Exp7/20.png)  

---

## Observations

- Jenkins GUI simplifies CI/CD management  
- GitHub acts as source + pipeline definition  
- Docker ensures consistent builds  
- Webhook enables automation  

---

## Result

Successfully implemented a complete CI/CD pipeline where:

- Source code and pipeline are maintained in GitHub  
- Jenkins automatically detects changes  
- Docker image is built on host agent  
- Image is securely pushed to Docker Hub

---

## Conclusion  

A CI/CD pipeline was successfully implemented using Jenkins, GitHub, and Docker Hub.  
The application was containerized using Docker and automatically built and deployed through Jenkins pipeline.
