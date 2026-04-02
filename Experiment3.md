# CONTAINERIZATION AND DEVOPS LAB

## Experiment 3:  
### Deploying Nginx using different base images and comparing image layers

**Reference Link:**  
https://upessocs.github.io/#dir=/Lectures/Containerization%20and%20DevOps/Theory/Containerization%20and%20DevOps/Lab/&file=Experiment%203%20Nginix.md

---

## Objective

1. Deploy NGINX using:
    <ul>
      <li>Official `nginx` image</li>
      <li>Ubuntu-based image</li>
      <li>Alpine-based image</li>
    </ul>
2. Understand Docker image layers and size differences
3. Compare performance, security, and use-cases of each approach
4. Explain real-world use of NGINX in containerized system

---

## Part A: Deploy Nginx using official image

### 0. Starting docker demon first
![Docker Demon](Images/Images%20Exp3/0a.png)

![Docker Demon](Images/Images%20Exp3/0b.png)

![Docker Demon](Images/Images%20Exp3/0c.png)

![Docker Demon](Images/Images%20Exp3/0d.png)

---

### 1. Pull the Image
![Pull image](Images/Images%20Exp3/1a.png)

---

### 2. Run Container
![run container](Images/Images%20Exp3/2a.png)

---

### 3. Verify
![verify](Images/Images%20Exp3/3a.png)

![verify](Images/Images%20Exp3/3b.png)

---

### 4. Key Observations
![observations](Images/Images%20Exp3/4a.png)

---


## Part B: Custom Nginx using Ubuntu base image

### 1. Create Dockerfile
![create dockerfile](Images/Images%20Exp3/1'a.png)

---

### 2. Change Directory
![change directory](Images/Images%20Exp3/2'a.png)

---

### 3. Build Image
![build image](Images/Images%20Exp3/3'a.png)

---

### 4. Run Container
![run container](Images/Images%20Exp3/4'a.png)

---

### 5. Observations
![observations](Images/Images%20Exp3/5'a.png)

---

## Part C: Custom Nginx using Alpine base image

### 1. Create Dockerfile
![create dockerfile](Images/Images%20Exp3/1''a.png)

---

### 2. Build Image
![build image](Images/Images%20Exp3/2''a.png)

---

### 3. Run Container
![run container](Images/Images%20Exp3/3''a.png)

---

### 4. Observations
![observations](Images/Images%20Exp3/4''a.png)

---

## Result

The experiment 

---

## Conclusion

Virtual Machines 
