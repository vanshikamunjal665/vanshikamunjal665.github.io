# CONTAINERIZATION AND DEVOPS LAB

## Experiment 1:  
### Comparison of Virtual Machines (VMs) and Containers using Ubuntu and Nginx

**Reference Link:**  
https://upessocs.github.io/#dir=/Lectures/Containerization%20and%20DevOps/Lab/&file=Experiment%201%20Compare%20VM%20with%20Container.md

---

## Objective

1. To understand the conceptual and practical differences between Virtual Machines and Containers.  
2. To install and configure a Virtual Machine using VirtualBox and Vagrant on Windows.  
3. To install and configure Containers using Docker inside WSL.  
4. To deploy an Ubuntu-based Nginx web server in both environments.  
5. To compare resource utilization, performance, and operational characteristics of Virtual Machines and Containers.

---

## Part A: Virtual Machine (Windows)

### 1. Install Vagrant for Windows and Verify Installation
![Vagrant Installation](Images/Images%20Exp1/1a.png)

![Vagrant Installation](Images/Images%20Exp1/1b.png)
---

### 2. Initialize Vagrant with Ubuntu Box
![Vagrant Installation](Images/Images%20Exp1/2a.png)

---

### 3. Start the Virtual Machine
![Vagrant Installation](Images/Images%20Exp1/3a.png)

![Vagrant Installation](Images/Images%20Exp1/3b.png)

---

### 4. Access the Virtual Machine
![Vagrant Installation](Images/Images%20Exp1/4a.png)

---

### 5. Install Nginx inside the Virtual Machine
![Vagrant Installation](Images/Images%20Exp1/5a.png)

![Vagrant Installation](Images/Images%20Exp1/5b.png)

![Vagrant Installation](Images/Images%20Exp1/5c.png)

---

### 6. Verify Nginx Installation
![Vagrant Installation](Images/Images%20Exp1/6a.png)

---

### 7. VM Observation Commands
![Vagrant Installation](Images/Images%20Exp1/7a.png)

![Vagrant Installation](Images/Images%20Exp1/7b.png)

![Vagrant Installation](Images/Images%20Exp1/7c.png)

---

### 8. Exit, Stop, and Remove the Virtual Machine
![Vagrant Installation](Images/Images%20Exp1/8a.png)

![Vagrant Installation](Images/Images%20Exp1/8b.png)

![Vagrant Installation](Images/Images%20Exp1/8c.png)

![Vagrant Installation](Images/Images%20Exp1/8d.png)

---

## Part B: Containers using WSL (Windows)

### 1. Install Docker Engine inside WSL
![Vagrant Installation](Images/Images%20Exp1/1'a.png)

![Vagrant Installation](Images/Images%20Exp1/1'b.png)

---

### 2. Run Ubuntu Container with Nginx
![Vagrant Installation](Images/Images%20Exp1/2'a.png)

---

### 3. Verify Nginx in Container
![Vagrant Installation](Images/Images%20Exp1/3'a.png)

---

### 4. Container Observation Commands
![Vagrant Installation](Images/Images%20Exp1/4'a.png)

![Vagrant Installation](Images/Images%20Exp1/4'b.png)

![Vagrant Installation](Images/Images%20Exp1/4'c.png)

---

## Result

The experiment demonstrates that containers are significantly more lightweight and resource-efficient compared to virtual machines, while virtual machines provide stronger isolation and full OS-level abstraction.

---

## Conclusion

Virtual Machines are suitable for full OS isolation and legacy workloads, whereas Containers are ideal for microservices, rapid deployment, and efficient resource utilization.
