# CONTAINERIZATION AND DEVOPS LAB

## Experiment 11:  
### Orchestration using Docker Compose & Docker Swarm (Continuation of Experiment 6)

**Reference Link:**  
https://upessocs.github.io/#dir=/Lectures/Containerization%20and%20DevOps/Lab/&file=Experiment%2011%20Container%20Orchestration%20with%20Docker%20Stack.md
---

# Theory

## PART A – CONCEPT CONTINUATION (Simple Explanation)

### From Experiment 6, we already know:

| Tool            | What it does                     | Limitation                         |
|-----------------|----------------------------------|------------------------------------|
| `docker run`    | Runs a single container          | Manual, no coordination            |
| Docker Compose  | Runs multiple containers together| Single machine, no auto-healing    |

---

### New Concept: Orchestration

**Orchestration = Automatic management of containers**

Think of it like a **restaurant manager**:

- Decides how many waiters are needed (**scaling**)  
- Replaces a sick waiter immediately (**self-healing**)  
- Distributes customers evenly (**load balancing**)  

---

### What Orchestration Adds:

| Feature        | What it means                                      |
|----------------|---------------------------------------------------|
| Scaling        | Increase/decrease number of containers            |
| Self-healing   | Restart failed containers automatically           |
| Load balancing | Distribute traffic across containers              |
| Multi-host     | Run containers across multiple machines           |

---

### Progression Path
```
docker run  →  Docker Compose  →  Docker Swarm  →  Kubernetes
     |             |                  |                 |
 Single        Multi-container     Orchestration    Advanced
 container     (single host)       (basic)          orchestration
```

---

## Part B: Practical (Extension of Experiment 6)

### 1. Create docker-compose.yml (from experiment 6)

We use the same docker-compose file created in Experiment 6 for WordPress and MySQL setup.

![Image](Images/Images%20Exp11/1.png)  

---

### 2. Stop any existing compose setup

This ensures no previous containers interfere with Swarm deployment.

```bash
docker compose down -v
```

![Image](Images/Images%20Exp11/2.png)  

---

### 3. Verify no containers are running

Check that all containers are stopped.

```bash
docker ps
```

![Image](Images/Images%20Exp11/3.png)  

---

### 4. Initialize Docker Swarm

This command enables swarm mode and makes the system a manager node.

```bash
docker swarm init --advertise-addr $(hostname -I | awk '{print $1}')
```

![Image](Images/Images%20Exp11/4.png)  

---

### 5. Verify Swarm is active

This shows the node status in the swarm.

```bash
docker node ls
```

![Image](Images/Images%20Exp11/5.png)  

---

### 6. Deploy as a Stack (not just Compose)

Deploy the application using swarm stack instead of docker compose.

```bash
docker stack deploy -c docker-compose.yml wpstack
```

![Image](Images/Images%20Exp11/6.png)  

---

### 7. Verify the deployment

Check all services created in the stack.

```bash
docker service ls
```

![Image](Images/Images%20Exp11/7.png)  

---

### 8. See detailed tasks (containers) for a service

Displays container-level details for a specific service.

```bash
docker service ps wpstack_wordpress
```

![Image](Images/Images%20Exp11/8.png)  

---

### 9. See all running containers

List all running containers.

```bash
docker ps
```

![Image](Images/Images%20Exp11/9.png)  

---

### 10. Access WordPress

Open the application in browser:

http://localhost:8080  

![Image](Images/Images%20Exp11/10.png)  

---

### 11. Scale the Application

Increase the number of WordPress containers.

```bash
docker service scale wpstack_wordpress=3
```

![Image](Images/Images%20Exp11/11.png)  

---

### 12. Verify scaling

Check if replicas increased successfully.

```bash
docker service ls
```

![Image](Images/Images%20Exp11/12.png)  

---

### 13. Test self-healing

### a. Kill the container (simulate crash)

Manually stop a container to test recovery.

```bash
docker kill <container_id>
```

![Image](Images/Images%20Exp11/13.png)  

### b. Watch swarm recreate it

Swarm automatically creates a new container.

```bash
docker service ps wpstack_wordpress
```

![Image](Images/Images%20Exp11/14.png)  

### c. Verify new container is running

```bash
docker ps
```

![Image](Images/Images%20Exp11/15.png)  

---

### 14. Remove the stack

Deletes all services in the stack.

```bash
docker stack rm wpstack
```

![Image](Images/Images%20Exp11/16.png)  

---

### 15. Verify removal

Ensure all services are removed.

```bash
docker service ls
```

![Image](Images/Images%20Exp11/17.png)  

---

## Conclusion

In this experiment, we extended Docker Compose by introducing Docker Swarm. We successfully deployed a multi-container application as a stack, scaled services, and observed self-healing behavior. This demonstrates how container orchestration automates deployment, scaling, and management of applications.
