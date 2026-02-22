# CONTAINERIZATION AND DEVOPS LAB

## Experiment 4:  
### Docker Essentials

**Reference Link:**  
https://upessocs.github.io/#dir=/Lectures/Containerization%20and%20DevOps/Lab/&file=Experiment%204%20Docker%20Essentials%20Dockerfile%20dockerignore%20tagging%20and%20publishing.md

---

## Objective

1. Dockerfile
2. .dockerignore
3. Tagging
4. Publishing

---

## Part 1: Containerization Applications with Dockerfile

### 1. Create a Simple Application
##### python flask app
![Image](Images/Images%20Exp4/1a.png)

##### app.py
![Image](Images/Images%20Exp4/1b.png)

##### requirements.txt
![Image](Images/Images%20Exp4/1c.png)

##### folders
![Image](Images/Images%20Exp4/1d.png)

---

### 2. Create Dockerfile
![Image](Images/Images%20Exp4/2a.png)

![Image](Images/Images%20Exp4/2b.png)

---


## Part 2: Using .dockerignore

### 1. Create .dockerignore File
![image](Images/Images%20Exp4/1''a.png)

##### folders
![image](Images/Images%20Exp4/1''b.png)
---

### Why .dockerignore is important?
1. Prevents unnecessary files from being copied  
2. Reduces image size  
3. Improves build speed  
4. Increases security  
---

## Part 3: Building Docker Images

### 1.	Build image from Dockerfile
![image](Images/Images%20Exp3/1'''a.png)

---

### 2. Check build images
![image](Images/Images%20Exp3/2'''a.png)

---

### 3. Tag with version number (alternative)
![image](Images/Images%20Exp3/3'''a.png)

---

### 4. Show image history
![image](Images/Images%20Exp3/4'''a.png)

---

### 5. Inspect image details
![image](Images/Images%20Exp3/5'''a.png)

---

## Part 4: Running Containers

### 1. Run container with port mapping
![image](Images/Images%20Exp4/1''''a.png)

---

### 2. Test the application
![image](Images/Images%20Exp4/2''''a.png)

![image](Images/Images%20Exp4/2''''b.png)
---

### 3. View running containers
![image](Images/Images%20Exp4/3''''a.png)

---

### 4. View container logs
![image](Images/Images%20Exp4/4''''a.png)

---

### 5. Stop container
![image](Images/Images%20Exp4/5''''a.png)

---

### 6. Start stopped container
![image](Images/Images%20Exp4/6''''a.png)

---

### 7. Remove container
![image](Images/Images%20Exp4/7''''a.png)

---

### 8. Remove container forcefully
![image](Images/Images%20Exp4/8''''a.png)

---

## Part 5: Multi-stage Builds

### Why Multi-stage Builds?
1. Smaller final image size
2. Better security (remove build tools)
3. Separate build and runtime environments


### 1. Simple multi-stage Dockerfile
![image](Images/Images%20Exp4/1'''''a.png)

---

### 2. Build regular image
![image](Images/Images%20Exp4/2'''''a.png)

---

### 3. Build multi-stage image
![image](Images/Images%20Exp4/3'''''a.png)

---

### 4. Compare sizes
![image](Images/Images%20Exp4/4'''''a.png)

---

## Part 6: Publishing to Docker Hub

### 1. Login to Docker Hub
![image](Images/Images%20Exp4/1''''''a.png)

---

### 2. Tag image for Docker Hub
![image](Images/Images%20Exp4/2''''''a.png)

---

### 3. Push to Docker Hub
![image](Images/Images%20Exp4/3''''''a.png)

---

### 4. Pull from Docker Hub
![image](Images/Images%20Exp4/4''''''a.png)

---

### 5. Run the pulled image
![image](Images/Images%20Exp4/5''''''a.png)

---

## Part 7: Node.js Example

### 1. Node.js Application
##### app.js
![Image](Images/Images%20Exp4/1'''''''a.png)

##### package.json
![Image](Images/Images%20Exp4/1'''''''b.png)

##### Dockerfile
![Image](Images/Images%20Exp4/1'''''''c.png)

##### folders
![Image](Images/Images%20Exp4/1'''''''d.png)

---

### 2. Build Image
![Image](Images/Images%20Exp4/2'''''''a.png)

---

### 3. Run container
![image](Images/Images%20Exp4/3'''''''a.png)

---

### 4. Test
![image](Images/Images%20Exp4/4'''''''a.png)

![image](Images/Images%20Exp4/4'''''''b.png)

---
