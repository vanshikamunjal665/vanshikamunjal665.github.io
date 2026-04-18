# CONTAINERIZATION AND DEVOPS LAB

## Experiment 10:  
### SonarQube

**Reference Link:**  
https://upessocs.github.io/#dir=/Lectures/Containerization%20and%20DevOps/Lab/&file=Experiment%2010%20SonarQube.md

---

# Theory

## Problem Statement
Managing infrastructure manually across multiple servers leads to configuration drift, inconsistent environments, and time-consuming repetitive tasks. Scaling from one server to hundreds becomes nearly impossible with manual SSH-based administration.

---

## What is Ansible?

- Ansible is an open-source **automation tool** for **configuration management, application deployment, and orchestration**.
- It follows an **agentless architecture**, using SSH for Linux and WinRM for Windows.
- Uses **YAML-based playbooks** to define automation tasks.

*Ansible is software that enables cross-platform automation and orchestration at scale and has become the standard choice among enterprise automation solutions.*

---

## How Ansible Solves the Problem

- **Agentless Architecture**: No software installation required on managed nodes  
- **Idempotency**: Running playbooks multiple times yields the same result  
- **Declarative Syntax**: Describe desired state, not the steps to achieve it  
- **Push-based**: Initiates changes from control node immediately  

---

## Key Concepts

| Component        | Description |
|----------------|------------|
| Control Node    | Machine with Ansible installed |
| Managed Nodes   | Target servers (no Ansible agent needed) |
| Inventory       | Defines the list of managed nodes (e.g., `inventory.ini`) |
| Playbooks       | YAML files containing a sequence of automation steps |
| Tasks           | Individual actions in playbooks (e.g., installing a package) |
| Modules         | Built-in functionality to perform tasks (e.g., `yum`, `apt`, `service`) |
| Roles           | Pre-defined reusable automation scripts |

---

## How does Ansible work?

Ansible uses the concepts of control and managed nodes. It connects from the **control node**, any machine with Ansible installed, to the **managed nodes**, sending commands and instructions to them. The units of code that Ansible executes on the managed nodes are called **modules**. Each module is invoked by a **task**, and an ordered list of tasks together forms a **playbook**. Users write playbooks with tasks and modules to define the desired state of the system. The managed machines are represented in a simple **inventory file** that groups all nodes into different categories. Ansible uses a simple language, **YAML**, to define playbooks in a human-readable format.  
*Ansible doesn’t require installation of any extra agents on managed nodes, making it easy to start using.*  
Typically, the only requirement is a terminal to execute commands and a text editor to define configuration files.

---

## Benefits of using Ansible

- A free and open-source community project with a huge audience  
- Battle-tested over many years as a preferred IT automation tool  
- Easy to start and use without needing special coding skills  
- Simple deployment workflow without extra agents  
- Supports modularity and reusability for advanced automation  
- Extensive official documentation with strong community support  

---

## 1. Create Experiment Directory

```bash
mkdir sonarqube-exp10
cd sonarqube-exp10
```

*(Insert Image)*  

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

*(Insert Image)*  

---

## 3. Start Container

```bash
docker-compose up -d
```

*(Insert Image)*  

---

## 4. Check Containers

```bash
docker ps
```
 
*(Insert Image)*  

---

## 5. Create Sample Java Application

### Create project folder

```bash
mkdir -p sample-java-app/src/main/java/com/example
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

*(Insert Image)*  

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

*(Insert Image)*  

---

## 7. Login to SonarQube and Generate Token

- Open: http://localhost:9000  
- Login: admin/admin  
- Go to My Account → Security  
- Generate Token  

*(Insert Image)*  

---

## 8. Create sonar-project.properties

```properties
sonar.projectKey=sample-java-app
sonar.projectName=Sample Java Application
sonar.sources=src
sonar.host.url=http://sonarqube:9000
sonar.login=YOUR_TOKEN
```

*(Insert Image)*  

---

## 9. Run SonarQube Scanner

```bash
docker exec sonar-scanner sonar-scanner \
-Dsonar.host.url=http://sonarqube:9000 \
-Dsonar.login=YOUR_TOKEN \
-Dsonar.projectKey=sample-java-app \
-Dsonar.sources=src
```

*(Insert Image)*  

---

## 10. Analyze Results

- Open SonarQube Dashboard  
- View Bugs, Vulnerabilities, Code Smells  
- Check Quality Gate  

*(Insert Image)*  

---

## 11. Generate Report using SonarQube API

```bash
curl -u YOUR_TOKEN: \
"http://localhost:9000/api/issues/search?projectKeys=sample-java-app&types=BUG"
```

*(Insert Image)*  

---

## Conclusion

SonarQube was successfully deployed using Docker and used to analyze a Java application. The tool detected bugs and code smells, and results were visualized through the dashboard and API.
