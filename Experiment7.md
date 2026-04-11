# CONTAINERIZATION AND DEVOPS LAB

## Experiment 7:  
### CI/CD using Jenkins, GitHub and Docker Hub

**Reference Link:**  
https://upessocs.github.io/#dir=/Lectures/Containerization%20and%20DevOps/Lab/&file=Experiment%2007%20CICD%20using%20Jenkins,%20GitHub%20and%20Docker%20Hub.md

---

# Part A: GitHub Repository Setup (Source Code + Build Definition)

## 1. Create Repository  
A GitHub repository named **my-app** was created to store the project files.

## 2. Project Structure  
The repository contains the following files:
- Dockerfile  
- Jenkinsfile  
- app.py  
- requirements.txt  
- README.md  

## 3. Application Code  
A simple Python application was created using Flask framework.

## 4. Dockerfile (Build Process)  
A Dockerfile was created to containerize the application and define the build steps.

## 5. Jenkinsfile (Pipeline Definition in GitHub)  
A Jenkinsfile was added to define the CI/CD pipeline including:
- Cloning repository  
- Building Docker image  
- Logging into Docker Hub  
- Pushing Docker image  

---

# Part B: Jenkins Setup using Docker (Persistent Configuration)

## 1. Create Docker Compose file  
A Docker Compose file was used to run Jenkins container with persistent storage.

## 2. Run Jenkins  
Jenkins was started using Docker and accessed via:  
http://localhost:8080  

## 3. Unlock Jenkins  
Jenkins was unlocked using the initial admin password from the container.

---

# Part C: Jenkins Configuration

## 1. Add Docker Hub Credentials  
Docker Hub access token was generated and added to Jenkins credentials securely.

## 2. Create Pipeline Job  
A pipeline job named **ci-cd-pipeline** was created and configured using the Jenkinsfile.

---

# Part D: Build Jenkins

## 1. Build  
The pipeline was executed successfully, performing the following steps:
- Cloned code from GitHub  
- Built Docker image  
- Logged into Docker Hub  
- Pushed image to Docker Hub  

## 2. Result  

### Fig 1: Jenkins Pipeline Success  
![image](image)

### Fig 2: Docker Image on Docker Hub  
![image](image)

---

# Conclusion  

A CI/CD pipeline was successfully implemented using Jenkins, GitHub, and Docker Hub.  
The application was containerized using Docker and automatically built and deployed through Jenkins pipeline.
