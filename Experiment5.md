# CONTAINERIZATION AND DEVOPS LAB

## Experiment 5:  
### Docker- Volumes, Environment Variables, Monitoring & Networks

**Reference Link:**  
https://upessocs.github.io/#dir=/Lectures/Containerization%20and%20DevOps/Lab/&file=Experiment%2005%20Docker%20Volumes,%20Environment%20Variables,%20Monitoring,%20Networks%20Final.md

---

## Part 1: Docker Volumes- Persistent Data Storage
### Lab 1: Understanding Data Persistence  


##### The Problem: Container Data is Ephemeral  
![Image](Images/Images%20Exp5/1a.png)  

Solution: Volumes

---

### Lab 2: Volume Types

1. Anonymous Volumes  
![Image](Images/Images%20Exp5/1b.png)


3. Named Volumes  
![Image](Images/Images%20Exp5/1c.png)

![Image](Images/Images%20Exp5/1d.png)  


3. Bind Mounts  
![Image](Images/Images%20Exp5/1e.png)


### Lab 3: Practical Volume Examples
#### Example 1: Database with Persistent Storage

![Image](Images/Images%20Exp5/1f.png)  


#### Example 2: Web App with Configuration Files

![Image](Images/Images%20Exp5/1g.png)  

![Image](Images/Images%20Exp5/1h.png)  

### Lab 4: Volume Management Commands

![Image](Images/Images%20Exp5/1i.png)  

![Image](Images/Images%20Exp5/1j.png)  

![Image](Images/Images%20Exp5/1k.png)  

## Part 2: Environment Variables
### Lab 1: Setting Environment Variables

##### Method 1: Using -e flag
![Image](Images/Images%20Exp5/2a.png)  

![Image](Images/Images%20Exp5/2b.png)  

![Image](Images/Images%20Exp5/2c.png)  

##### Method 2: Using --env-file
![Image](Images/Images%20Exp5/2d.png)  

![Image](Images/Images%20Exp5/2e.png)  


##### Method 3: In Dockerfile
Set default environment variables  
ENV NODE_ENV=production  
ENV PORT=3000  
ENV APP_VERSION=1.0.0  

## Part 3: Docker Monitoring
### Lab 1: Basic Monitoring Commands

![Image](Images/Images%20Exp5/3a.png)  

![Image](Images/Images%20Exp5/3b.png)  

![Image](Images/Images%20Exp5/3c.png)  

![Image](Images/Images%20Exp5/3d.png)  

![Image](Images/Images%20Exp5/3e.png)  

![Image](Images/Images%20Exp5/3f.png)  

![Image](Images/Images%20Exp5/3g.png)  

### Lab 2: docker top- Process Monitoring

![Image](Images/Images%20Exp5/3h.png)  

### Lab 3: docker logs- Application Logs

![Image](Images/Images%20Exp5/3i.png)  

![Image](Images/Images%20Exp5/3j.png)  

![Image](Images/Images%20Exp5/3k.png)  

![Image](Images/Images%20Exp5/3l.png)  

### Lab 4: Container Inspection

![Image](Images/Images%20Exp5/3m.png)  

![Image](Images/Images%20Exp5/3n.png)  

### Lab 5: Practical Monitoring Script

![Image](Images/Images%20Exp5/3o.png)  

![Image](Images/Images%20Exp5/3p.png)  

## Part 4: Docker Networks
### Lab 1: Understanding Docker Network Types

![Image](Images/Images%20Exp5/4a.png)  

### Lab 2: Network Types Explained
1. Bridge Network  
![Image](Images/Images%20Exp5/4b.png)

![Image](Images/Images%20Exp5/4c.png)  


2. Host Network  
![Image](Images/Images%20Exp5/4d.png)  


3. None Network  
![Image](Images/Images%20Exp5/4e.png)


5. Overlay Network (swarm)  
![Image](Images/Images%20Exp5/4f.png)  

### Lab 3: Network Management Commands

![Image](Images/Images%20Exp5/4g.png)  

### Lab 4: Multi-container Application Program

![Image](Images/Images%20Exp5/4h.png)  

![Image](Images/Images%20Exp5/4i.png)  

![Image](Images/Images%20Exp5/4j.png)  

### Lab 5: Network Inspection & Debugging

![Image](Images/Images%20Exp5/4k.png)  

![Image](Images/Images%20Exp5/4l.png)  

![Image](Images/Images%20Exp5/4m.png)  

![Image](Images/Images%20Exp5/4n.png)  

### Lab 6: Port Publishing vs Exposing

![Image](Images/Images%20Exp5/4o.png)  

![Image](Images/Images%20Exp5/4p.png)  

## Part 5: Complete Real-world Example

##### Implementation:

![Image](Images/Images%20Exp5/5a.png)  

![Image](Images/Images%20Exp5/5b.png)  

---

## Key Takeaways
1. Volumes persist data beyond container lifecycle  
2. Environment variables configure containers dynamically  
3. Monitoring commands help debug and optimize containers  
4. Networks enable secure container communication  
5. Always use named volumes for production data  
6. Custom networks provide better isolation and DNS  
7. Monitor resource usage to prevent issues  
8. Use .env files for sensitive configuration  

This experiment covers essential Docker features for building, configuring, and managing production-ready containerized applications.
