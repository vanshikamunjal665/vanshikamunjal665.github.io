# CONTAINERIZATION AND DEVOPS LAB

## Experiment 6A:  
### Comparison of Docker Run and Docker Compose

**Reference Link:**  
https://upessocs.github.io/#dir=/Lectures/Containerization%20and%20DevOps/Lab/&file=Experiment%2006%20Docker%20Compose%20vs%20Docker%20Run,%20and%20MultiContainer%20Application%20-%20Wordpress+MySQL.md

---

## Part A: Theory
### 1. Objective

To understand the relationship between `docker run` and Docker Compose, and to compare their configuration syntax and use cases.

---

### 2. Background Theory

#### 2.1 Docker Run (Imperative Approach)

The `docker run` command is used to create and start a container from an image. It requires explicit flags for:

- Port mapping (`-p`)
- Volume mounting (`-v`)
- Environment variables (`-e`)
- Network configuration (`--network`)
- Restart policies (`--restart`)
- Resource limits (`--memory`, `--cpus`)
- Container name (`--name`)

This approach is **imperative**, meaning you specify step-by-step instructions.

#### Example:
```bash
docker run -d \
  --name my-nginx \
  -p 8080:80 \
  -v ./html:/usr/share/nginx/html \
  -e NGINX_HOST=localhost \
  --restart unless-stopped \
  nginx:alpine
```

---

#### 2.2 Docker Compose (Declarative Approach)

Docker Compose uses a YAML file (`docker-compose.yml`) to define services, networks, and volumes in a structured format.

Instead of multiple `docker run` commands, a single command is used:

```bash
docker compose up -d
```

Compose is **declarative**, meaning you define the desired state of the application.

#### Equivalent Compose File:
```yaml
version: '3.8'

services:
  nginx:
    image: nginx:alpine
    container_name: my-nginx
    ports:
      - "8080:80"
    volumes:
      - ./html:/usr/share/nginx/html
    environment:
      NGINX_HOST: localhost
    restart: unless-stopped
```

---

### 3. Mapping: Docker Run vs Docker Compose

| Docker Run Flag       | Docker Compose Equivalent              |
|----------------------|----------------------------------------|
| `-p 8080:80`         | `ports:`                               |
| `-v host:container`  | `volumes:`                             |
| `-e KEY=value`       | `environment:`                          |
| `--name`             | `container_name:`                       |
| `--network`          | `networks:`                             |
| `--restart`          | `restart:`                              |
| `--memory`           | `deploy.resources.limits.memory`        |
| `--cpus`             | `deploy.resources.limits.cpus`          |
| `-d`                 | `docker compose up -d`                  |

---

### 4. Advantages of Docker Compose

1. Simplifies multi-container applications  
2. Provides reproducibility  
3. Version controllable configuration  
4. Unified lifecycle management  
5. Supports service scaling  

#### Example:
```bash
docker compose up --scale web=3
```

## Part B: Practical Task

#### Task 1: Single Container Comparison

**Step 1: Run Nginx using Docker Run**  
![Image](Images/Images%20Exp5/5b.png)  

![Image](Images/Images%20Exp5/5b.png)  

![Image](Images/Images%20Exp5/5b.png)  

![Image](Images/Images%20Exp5/5b.png)  

**Step 2: Run same setup using Docker Compose**  
![Image](Images/Images%20Exp5/5b.png)  

![Image](Images/Images%20Exp5/5b.png)  

---

#### Task 2: Multi-container Application

**Objective:**  
Deploy WordPress with MySQL using:

1. Docker Run (manual way)  
2. Docker Compose (structured way)  

---

### I. Using Docker Run

1. Create Network
![Image](Images/Images%20Exp5/5b.png)  

3. Run MySQL  
![Image](Images/Images%20Exp5/5b.png)  

4. Run WordPress  
![Image](Images/Images%20Exp5/5b.png)  

5. Test  
![Image](Images/Images%20Exp5/5b.png)  

---

### II. Using Docker Compose

1. Create docker-compose.yml
![Image](Images/Images%20Exp5/5b.png)  

3. Run  
![Image](Images/Images%20Exp5/5b.png)

![Image](Images/Images%20Exp5/5b.png)  

5. Stop
![Image](Images/Images%20Exp5/5b.png)  

---

## Part C: Conversion and Build-based Tasks

### Task 3: Convert Docker Run to Docker Compose

**Problem 1: Basic Web Application**  
![Image](Images/Images%20Exp5/5b.png)  

![Image](Images/Images%20Exp5/5b.png)  

![Image](Images/Images%20Exp5/5b.png)  


**Problem 2: Volume + Network Configuration**  
![Image](Images/Images%20Exp5/5b.png)  

![Image](Images/Images%20Exp5/5b.png)  

![Image](Images/Images%20Exp5/5b.png)  

---

### Task 4: Resource Limits Conversion

![Image](Images/Images%20Exp5/5b.png)  

![Image](Images/Images%20Exp5/5b.png)  

![Image](Images/Images%20Exp5/5b.png)  

**Note:**  
When deploy works: The deploy section works only in Docker Swarm mode and is ignored in normal docker-compose.
Difference between Compose and Swarm: Docker Compose is used for local development, while Docker Swarm is used for production and supports features like resource limits and scaling.

---

## Part D: Using Dockerfile instead of Standard Image

### Task 5: Replace Standard Image with Dockerfile (Node App)  
![Image](Images/Images%20Exp5/5b.png)  

![Image](Images/Images%20Exp5/5b.png)  

![Image](Images/Images%20Exp5/5b.png)  

1. Build and Run
![Image](Images/Images%20Exp5/5b.png)  

2. Verify in Browser  
![Image](Images/Images%20Exp5/5b.png)  

3. Modify `app.js` message  
![Image](Images/Images%20Exp5/5b.png)  

4. Rebuild and observe changes  
![Image](Images/Images%20Exp5/5b.png)

![Image](Images/Images%20Exp5/5b.png)  

---

5. Difference between Image and Build

**Image:**
- Used to pull a pre-built image from Docker Hub (or registry)  
- No need for Dockerfile  
- Faster to run  

**Build:**
- Used to create a custom image using a Dockerfile  
- Requires source code + Dockerfile  
- Allows customization  

---

### Task 6: Multistage Dockerfile with Compose

1. Create `app.js`
![Image](Images/Images%20Exp5/5b.png)  

2. Create multistage Dockerfile  
![Image](Images/Images%20Exp5/5b.png)  

3. Create docker-compose.yml  
![Image](Images/Images%20Exp5/5b.png)  

4. Build and run  
![Image](Images/Images%20Exp5/5b.png)

![Image](Images/Images%20Exp5/5b.png)  

5. Verify in browser
![Image](Images/Images%20Exp5/5b.png)    

6. Compare image size
![Image](Images/Images%20Exp5/5b.png)  

The multi-stage Docker build was implemented successfully. However, the final image size is approximately the same as the base image (127MB). This is because the application is very simple and does not include additional dependencies or build tools.  

In real-world applications, multi-stage builds significantly reduce image size by removing unnecessary build dependencies and keeping only the runtime environment.  

---

## Experiment 6B: Multi-container Application using Docker Compose (WordPress + Database)

### Objective

To deploy a multi-container application using Docker Compose, consisting of:

- WordPress (frontend + PHP)  
- MySQL database (backend)  

Also:

- Understand container networking & volumes  
- Learn how to scale services  
- Compare with Docker Swarm for production deployment  

---

### Steps

1. Create project directory  
![Image](Images/Images%20Exp5/5b.png)

![Image](Images/Images%20Exp5/5b.png)  

2. Create docker-compose.yml  
![Image](Images/Images%20Exp5/5b.png)  

3. Start Application  
![Image](Images/Images%20Exp5/5b.png)  

4. Verify in browser  
![Image](Images/Images%20Exp5/5b.png)  

5. Verify containers  
![Image](Images/Images%20Exp5/5b.png)  

6. Check volumes  
![Image](Images/Images%20Exp5/5b.png)  

7. Stop Application  
![Image](Images/Images%20Exp5/5b.png)  

---

### Scaling in Docker Compose

![Image](Images/Images%20Exp5/5b.png)  

![Image](Images/Images%20Exp5/5b.png)  
