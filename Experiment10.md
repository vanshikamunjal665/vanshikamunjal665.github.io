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

# Part A: Ansible Installation

## 1. Install via apt (Debian/Ubuntu)

![Image](Images/Images%20Exp9/1.png)  

![Image](Images/Images%20Exp9/2.png)  

![Image](Images/Images%20Exp9/3.png)  

Updates the system package listand ensures latest versions are available  
  ``sudo apt update``
  
Installs Ansible on your system and -y auto-confirms installation  
  ``sudo apt install ansible -y``

Checks if Ansible is installed properly and displays version and config details  
  ``ansible --version``

---

## 2. Post Installation Check

![Image](Images/Images%20Exp9/4.png)  


Tests Ansible on your own system (control node) and Checks if Ansible is working properly before connecting to other servers  
  ``ansible localhost -m ping``

---

# Part B: Create Docker Image and Test SSH Login

## 1. Create SSH key pair in WSL

![Image](Images/Images%20Exp9/5.png)  

    ssh-keygen -t rsa -b 4096

**Explanation:** Generates SSH keys.

---

## 2. Copy keys to current folder

![Image](Images/Images%20Exp9/6.png)  

    cp ~/.ssh/id_rsa.pub .
    cp ~/.ssh/id_rsa .

**Explanation:** Copies keys to working directory.

---

## 3. Check if copied

![Image](Images/Images%20Exp9/7.png)  

    ls

**Explanation:** Verifies files.

---

## 4. Copying keys to another directory

![Image](Images/Images%20Exp9/8.png)  

    cd /mnt/c/Users/Vanshika\ Munjal/Desktop/C\&D\ Lab/exp9\ file
    cp /mnt/c/Users/HP/id_rsa .
    cp /mnt/c/Users/HP/id_rsa.pub .

## 5. Create Dockerfile for Ubuntu SSH Server

![Image](Images/Images%20Exp9/9.png)  

![Image](Images/Images%20Exp9/10.png)  


**Explanation:** Sets up SSH-enabled Ubuntu container.

---

## 6. Build Docker Image

![Image](Images/Images%20Exp9/11.png)  

![Image](Images/Images%20Exp9/12.png)  

    docker build -t ubuntu-server .

**Explanation:** Builds Docker image.

---

## 7. Run Docker Container

![Image](Images/Images%20Exp9/13.png)  

    docker run -d -p 2222:22 --name ssh-test-server ubuntu-server

**Explanation:** Runs container with SSH.

---

## 8. Find Container IP Address

![Image](Images/Images%20Exp9/14.png)  

    docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' ssh-test-server

**Explanation:** Gets container IP.

---

## 9. Test SSH Connections

### Password Authentication

![Image](Images/Images%20Exp9/15.png)  

    ssh root@localhost -p 2222

### Key-Based Authentication

![Image](Images/Images%20Exp9/16.png)  

    ssh -i ~/.ssh/id_rsa root@localhost -p 2222

**Explanation:** Tests SSH login.

---

## 10. Cleanup

![Image](Images/Images%20Exp9/17.png)  

    docker stop ss-test-server
    docker rm -f ssh-test-server

---

# Part C: Ansible with Docker

## 1. Start Multiple Containers to act as a server

![Image](Images/Images%20Exp9/18.png)  

![Image](Images/Images%20Exp9/19.png)  

    for i in {1..4}; do
      docker run -d -p 220${i}:22 --name server${i} ubuntu-server
    done

**Explanation:** Creates 4 server containers.

---

## 2. Create Ansible Inventory

![Image](Images/Images%20Exp9/20.png)  

    echo "[servers]" > inventory.ini
    for i in {1..4}; do
      docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' server${i} >> inventory.ini
    done

**Explanation:** Adds server IPs.

---

## 3. Add Variables

![Image](Images/Images%20Exp9/20.png)  

    cat << EOF >> inventory.ini

    [servers:vars]
    ansible_user=root
    ansible_ssh_private_key_file=~/.ssh/id_rsa
    ansible_python_interpreter=/usr/bin/python3
    EOF

**Explanation:** Defines connection settings.

---

## 4. Review content of inventory.in

![Image](Images/Images%20Exp9/21.png)  

    cat inventory.ini

---

## 5. Manual SSH Test

![Image](Images/Images%20Exp9/22.png)  

    ssh -i ~/.ssh/id_rsa root@<IP>

---

## 6. Ansible Ping Test

![Image](Images/Images%20Exp9/23.png)  

    ansible all -i inventory.ini -m ping

**Explanation:** Checks connectivity.

---

## 7. Create Playbook (update.yml)

![Image](Images/Images%20Exp9/24.png)  

---

## 8. Run Playbook

![Image](Images/Images%20Exp9/25.png)  

    ansible-playbook -i inventory.ini update.yml

---

## 9. Verify Changes using Ansible

![Image](Images/Images%20Exp9/26.png)  

    ansible all -i inventory.ini -m command -a "cat /root/ansible_test.txt"

---

## 10. Verify changes manually via Docker

![Image](Images/Images%20Exp9/27.png)  

    for i in {1..4}; do
      docker exec server${i} cat /root/ansible_test.txt
    done

---

## 11. Cleanup

![Image](Images/Images%20Exp9/28.png)  

    for i in {1..4}; do docker rm -f server${i}; done

---

# ✅ Conclusion

In this experiment, Docker containers were used as servers and configured using Ansible. SSH authentication was implemented, an inventory file was created, and automation was achieved using playbooks across multiple nodes.
