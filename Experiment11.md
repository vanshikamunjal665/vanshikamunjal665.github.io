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

# PART A – CONCEPT CONTINUATION (Simple Explanation)

## 1. Create Experiment Directory

```bash
mkdir sonarqube-exp10
cd sonarqube-exp10
```

![Image](Images/Images%20Exp10/1.png)  

---

## 2. Create docker-compose.yml

```yaml
version: '3.8'

services:
  sonar-db:
    image: postgres:13
    container_name: sonar-db
    restart: unless-stopped
    environment:
      POSTGRES_USER: sonar
      POSTGRES_PASSWORD: sonar
      POSTGRES_DB: sonarqube
    volumes:
      - sonar-db-data:/var/lib/postgresql/data
    networks:
      - sonarqube-lab

  sonarqube:
    image: sonarqube:lts-community
    container_name: sonarqube
    restart: unless-stopped
    depends_on:
      - sonar-db
    ports:
      - "9000:9000"
    environment:
      SONAR_JDBC_URL: jdbc:postgresql://sonar-db:5432/sonarqube
      SONAR_JDBC_USERNAME: sonar
      SONAR_JDBC_PASSWORD: sonar
    volumes:
      - sonar-data:/opt/sonarqube/data
      - sonar-extensions:/opt/sonarqube/extensions
    networks:
      - sonarqube-lab

volumes:
  sonar-db-data:
  sonar-data:
  sonar-extensions:

networks:
  sonarqube-lab:
    driver: bridge
```

![Image](Images/Images%20Exp10/2.png)  

![Image](Images/Images%20Exp10/3.png)  

---

## 3. Start Container

```bash
docker-compose up -d
```

![Image](Images/Images%20Exp10/4.png)  

---

## 4. Check Containers

```bash
docker ps
```
 
![Image](Images/Images%20Exp10/5.png)  

---

## 5. Create Sample Java Application

### Create project folder

```bash
mkdir -p sample-java-app/src/main/java/com/example
cd sample-java-app
```

### Create Java File

```java
package com.example;

import java.util.ArrayList;
import java.util.List;

public class Calculator {

    public int divide(int a, int b) {
        return a / b;
    }

    public int add(int a, int b) {
        int result = a + b;
        int unused = 100;
        return result;
    }

    public String getUser(String userId) {
        String query = "SELECT * FROM users WHERE id = " + userId;
        return query;
    }

    public int multiply(int a, int b) {
        int result = 0;
        for (int i = 0; i < b; i++) {
            result = result + a;
        }
        return result;
    }

    public int multiplyAlt(int a, int b) {
        int result = 0;
        for (int i = 0; i < b; i++) {
            result = result + a;
        }
        return result;
    }

    public void processUser(String name, String email, String phone,
                           String address, String city, String state,
                           String zip, String country) {
        System.out.println("Processing: " + name);
    }

    public String getName(String name) {
        return name.toUpperCase();
    }

    public void riskyOperation() {
        try {
            int x = 10 / 0;
        } catch (Exception e) {
        }
    }
}
```

![Image](Images/Images%20Exp10/6.png)  

![Image](Images/Images%20Exp10/7.png)  

![Image](Images/Images%20Exp10/8.png)  

---

## 6. Install SonarQube Scanner

```bash
docker run -d \
--name sonar-scanner \
--network sonarqube-exp10_sonarqube-lab \
-v "$(pwd)/sample-java-app":/usr/src \
sonarsource/sonar-scanner-cli:latest \
sleep infinity
```

![Image](Images/Images%20Exp10/9.png)  

---

## 7. Login to SonarQube and Generate Token

- Open: http://localhost:9000  
- Login: admin/admin  
- Go to My Account → Security  
- Generate Token  

![Image](Images/Images%20Exp10/10.png)  

![Image](Images/Images%20Exp10/11.png)  

---

## 8. Create sonar-project.properties

```properties
sonar.projectKey=sample-java-app
sonar.projectName=Sample Java Application
sonar.sources=src
sonar.host.url=http://sonarqube:9000
sonar.login=YOUR_TOKEN
```

![Image](Images/Images%20Exp10/12.png)  

![Image](Images/Images%20Exp10/13.png)  

---

## 9. Run SonarQube Scanner

```bash
docker exec sonar-scanner sonar-scanner \
-Dsonar.host.url=http://sonarqube:9000 \
-Dsonar.login=YOUR_TOKEN \
-Dsonar.projectKey=sample-java-app \
-Dsonar.sources=src
```

![Image](Images/Images%20Exp10/14.png)  

---

## 10. Analyze Results

- Open SonarQube Dashboard  
- View Bugs, Vulnerabilities, Code Smells  
- Check Quality Gate  

![Image](Images/Images%20Exp10/15.png)  

![Image](Images/Images%20Exp10/16.png)  

---

## 11. Generate Report using SonarQube API

```bash
curl -u YOUR_TOKEN: \
"http://localhost:9000/api/issues/search?projectKeys=sample-java-app&types=BUG"
```

![Image](Images/Images%20Exp10/17.png)  

---

## Conclusion

SonarQube was successfully deployed using Docker and used to analyze a Java application. The tool detected bugs and code smells, and results were visualized through the dashboard and API.
