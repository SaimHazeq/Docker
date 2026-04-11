## 🐳 Docker & Containerization Guide
## 📌 Overview

This repository contains structured notes and hands-on commands for understanding Docker, containerization, and orchestration concepts used in modern DevOps environments.

## 🏗️ Application Architectures
**Monolithic Architecture**                                                      
- All services run on a single server                                            
- Uses a single database                                                         
- Simple but hard to scale and maintain

**Microservices Architecture**                                
- Services are distributed across multiple servers                               
- Each service may have its own database                                         
- Scalable and flexible but increases complexity                          

⚠️ Choose architecture based on:
- Application complexity                                                        
- User load                                                                      
- Cost                                                                        
- Maintenance overhead                                                             
## 📦 Containers
- Lightweight, isolated environments to run applications                         
- Share the host OS kernel (unlike VMs)                                          
- Faster and more efficient than virtual machine

**✅ Key Idea:**                                                               
Server (VM) ≠ Container                                                    
- VM → Full OS                                                                   
- Container → Uses host OS                                                       
## 🐳 Docker
- Open-source platform for containerization                                      
- Written in Go                                                                  
- Released in 2013 by Solomon Hykes                                              
- Enables building, shipping, and running applications consistently
**Key Features**                                                                 
- Platform-independent                                                           
- Uses host system resources (CPU, Memory, Network)                              
- Works best on Linux-based systems                                              
## 📦 Containerization
Packaging an application with all its dependencies.                             
Example:
- App → PUBG
- Dependency → Maps 
## 🖥️ Virtualization
Creating virtual resources (VMs) using physical hardware.  
## ⚙️ Docker Architecture
- Client → Sends commands                                                        
- Docker Daemon → Manages containers, images                                     
- Host → System where Docker runs                                               
- Registry → Stores Docker images (e.g., Docker Hub)                             
## 🚀 Basic Installation (Linux)
```bash
apt install docker -y
systemctl start docker
systemctl status docker
```
## 🔧 Common Docker Commands
```bash
docker pull ubuntu              # Pull image
docker images                   # List images
docker run -it ubuntu           # Run container
docker ps -a                    # List containers
docker stop <container>         # Stop container
docker start <container>        # Start container
docker rm <container>           # Remove container
docker rmi <image>              # Remove image
```
## 🧪 Inside Container (Ubuntu Example)
```bash
apt update -y
apt install git -y
apt install apache2 -y
service apache2 start
```
## 🏗️ Image Creation (Commit Method)
```bash
docker run -it ubuntu
apt update -y
apt install apache2 -y

docker commit <container_id> custom_image:v1
docker run -it custom_image:v1
```
## 📄 Dockerfile

Automated way to build Docker images.                                                    

| Instruction | Description                   |
| ----------- | ----------------------------- |
| FROM        | Base image                    |
| RUN         | Execute commands during build |
| CMD         | Default command               |
| ENTRYPOINT  | Main command                  |
| COPY        | Copy local files              |
| ADD         | Copy files (supports URLs)    |
| WORKDIR     | Set working directory         |
| ENV         | Environment variables         |
| EXPOSE      | Define port                   |

**Example Dockerfile:**
```bash
FROM ubuntu

RUN apt update -y && \
    apt install -y apache2

COPY index.html /var/www/html/

CMD ["/usr/sbin/apachectl", "-D", "FOREGROUND"]
```
**Build & Run**
```bash
docker build -t myapp:v1 .
docker run -d -p 80:80 myapp:v1
```
## 💾 Docker Volumes

Used for persistent storage.

**Create Volume**
```
docker volume create myvolume
```
**Use Volume**
```
docker run -it -v myvolume:/data ubuntu
```
## 📊 Docker System Commands
```
docker system df
docker system prune
docker inspect <container>
```
## ⚡ Resource Limits
```
docker run -d \
  --memory="200m" \
  --cpus="0.5" \
  ubuntu
```
## 🧩 Docker Compose

Used to manage multi-container applications.                                    

**Example** docker-compose.yml
```
version: "3.8"

services:
  web:
    image: nginx
    ports:
      - "80:80"

  app:
    image: myapp:v1
    ports:
      - "8080:80"
```
**Commands**
```
docker-compose up -d
docker-compose down
docker-compose ps
docker-compose logs
```
## 📤 Docker Hub

Push images to remote registry.
```
docker login
docker tag myapp username/myapp
docker push username/myapp
docker pull username/myapp
```
## 🧠 High Availability
- Multiple servers running the same app                                          
- Ensures uptime if one server fails                                            
## 🐝 Docker Swarm

Container orchestration tool.                                                    

**Key Concepts**                                                        
- **Manager Node** → Controls cluster
- **Worker Node** → Runs containers

**Initialize Swarm**
```
docker swarm init
```
**Deploy Service**
```
docker service create \
  --name web \
  --replicas 3 \
  -p 80:80 nginx
```
## 🔄 Service Commands
```
docker service ls
docker service scale web=5
docker service rm web
```
## 🌐 Docker Networking
| Type    | Description         |
| ------- | ------------------- |
| Bridge  | Default (same host) |
| Overlay | Multi-host          |
| Host    | Shares host network |
| None    | No network          |

**Example**
```
docker network create mynet
docker network connect mynet container1
```
## ⚠️ Key Notes
- Containers are ephemeral → use volumes for persistence                         
- Prefer Dockerfile over manual commits                                          
- Use Compose for multi-container setups                                        
- Use Swarm/Kubernetes for production orchestration                
## 📚 Summary

This guide covers:                                                            

- Docker fundamentals                                                            
- Container lifecycle                                                            
- Image creation                                                                 
- Volumes & networking                                                           
- Compose & Swarm                                                                  
