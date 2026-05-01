# CONTAINERIZATION AND DEVOPS LAB

## Experiment 12:  
### Study and analyse container orchestration using Kubernetes

**Reference Link:**  
https://upessocs.github.io/#dir=/Lectures/Containerization%20and%20DevOps/Lab/&file=Experiment%2012%20Kubernets%20Draft.md
---

## Theory

### Objective

Learn why Kubernetes is used, its basic concepts, and how to deploy, scale, and fix apps using Kubernetes commands.

---

#### Why Kubernetes over Docker Swarm?

| Reason                | Explanation                                      |
|---------------------|--------------------------------------------------|
| Industry standard    | Most companies use Kubernetes                   |
| Powerful scheduling | Automatically decides where to run your app     |
| Large ecosystem     | Many tools and plugins available                |
| Cloud-native support| Works on AWS, Google Cloud, Azure, etc.         |

---

#### Core Kubernetes Concepts (Simple Explanation)

| Docker Concept   | Kubernetes Equivalent | What it means |
|----------------|---------------------|--------------|
| Container      | **Pod**             | A pod is a group of one or more containers. Smallest unit in K8s. |
| Compose service| **Deployment**      | Describes how your app should run (e.g., number of copies, image used) |
| Load balancing | **Service**         | Exposes your app to the outside world or other pods |
| Scaling        | **ReplicaSet**      | Ensures a certain number of pod copies are always running |

---

## Task 1: Create a Deployment

### Step 1: Create a file (wordpress-deployment.yaml)

![Image](Images/Images%20Exp12/1.png)  

---

### Step 2: Apply the deployment

```bash
kubectl apply -f wordpress-deployment.yaml
```

![Image](Images/Images%20Exp12/2.png)  

**What happens?** Kubernetes creates 2 pods running WordPress.

---

### Step 3: Check if pods are running

```bash
kubectl get pods
```

![Image](Images/Images%20Exp12/3.png)  

---

### Step 4: Check deployment status

```bash
kubectl get deployments
```

![Image](Images/Images%20Exp12/4.png)  

---

## Task 2: Expose the deployment as a service

Pods are temporary (they can be deleted or recreated). A service gives them a fixed IP and exposes them to the outside.

---

### Step 1: Create a file (wordpress-service.yaml)

![Image](Images/Images%20Exp12/5.png)  

---

### Step 2: Apply the service

```bash
kubectl apply -f wordpress-service.yaml
```

![Image](Images/Images%20Exp12/6.png)  

---

### Step 3: Services running in cluster

```bash
kubectl get services
```

![Image](Images/Images%20Exp12/7.png)  

---

## Task 3: Verify everything

### Step 1: Check pods

```bash
kubectl get pods
```

![Image](Images/Images%20Exp12/8.png)  

---

### Step 2: Check service

```bash
kubectl get svc
```

![Image](Images/Images%20Exp12/9.png)  

---

### Step 3: Access WordPress in browser

```bash
kubectl port-forward service/wordpress-service 8080:80
```

Open in browser:  
http://localhost:8080  

![Image](Images/Images%20Exp12/10.png)  

---

## Task 4: Scale the deployment

### Step 1: Increase replicas

```bash
kubectl scale deployment wordpress --replicas=4
```

![Image](Images/Images%20Exp12/11.png)  

---

### Step 2: Verify scaling

```bash
kubectl get pods
```

![Image](Images/Images%20Exp12/12.png)  

---

## Task 5: Self-healing demonstration

Kubernetes automatically replaces failed pods.

---

### Step 1: Delete one pod manually

```bash
kubectl delete pod <pod-name>
```

![Image](Images/Images%20Exp12/13.png)  

---

### Step 2: Check pods again

```bash
kubectl get pods
```

![Image](Images/Images%20Exp12/14.png)  

**Result:** The deleted pod is automatically recreated.

---

# Result
- Successfully deployed WordPress using Kubernetes  
- Exposed application using Service  
- Verified deployment and service  
- Scaled application from 2 to 4 pods  
- Demonstrated self-healing  

---

# Conclusion
Kubernetes simplifies container orchestration by providing automated deployment, scaling, load balancing, and self-healing, ensuring high availability of applications.
