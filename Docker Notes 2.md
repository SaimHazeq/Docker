# DOCKER

**APPLICATION:**                                                          
Collection of Service

**MONOLITHIC:**                                                          
Multiple services are deployed on single server with single database.

**MICRO SERVICES:**                                                      
Multiple services are deployed on multiple servers with multiple databases.

**BASED ON USERS AND APP COMPLEXITY WE NEED TO SELECT THE ARCHITECTURE.**

FACTORS AFFECTING FOR USING MICRO SERVICES:                               
F-1 : COST                                                             
F-2 : MAINTAINANCE

## **CONTAINERS:**
- It’s same as a server/vm.
- It will not have any operating system.
- OS will be on images.
- (SERVER=AMI, CONTAINER=IMAGE)
- It’s free of cost and can create multiple containers.

## **DOCKER:**
- It’s an free & open-source.
- It is platform independent.
- Used to create, run & deploy applications on containers.
- It is introduced on 2013 by solomen hykes & Sebastian phal.
- We used GO language to develop the Docker.
- Here we write files on YAML.
- Before Docker user faced lot of problems, but after Docker there is no issues with the application.
- Docker will use host resources (cpu, mem, n/w, os).
- Docker can run on any OS but it natively supports Linux distributions.

## **CONTAINERIZATION:**
Process of packing an application with its dependencies.                    
Ex: PUBG                                                                 
APP = PUBG & DEPENDENCY = MAPS                                            
APP = CAKE & DEPENDENCY = KNIFE

## **VIRTUALIZATION:**
Able to create resource with our hardware properties.

## **ARCHITECTURE & COMPONENTS:**
Client: it will interact with user                                          
User gives commands and it will be executed by docker client

**Deamon**:   Manages the Docker components (images, containers, volumes)   
**Host**:     Where we install Docker (ex: linux, windows, macOS)           
**Registry**: Manages the images.

## **ARCHITECTURE OF DOCKER:**
```bash
yum install docker -y #client
systemctl start docker #client, Engine
systemctl status docker
```

COMMANDS:

```bash
docker pull ubuntu    #pull ubuntu image
docker images         #to see list of images
docker run –it --name cont1 ubuntu   #to create a container
-it (interactive)     #to go inside a container
cat /etc/os-release   #to see os flavor
apt update -y         #to update
```
redhat = yum                                                              
ubuntu = apt                                                               
Without update we can’t install any pkg in Ubuntu

```bash
apt install git -y
apt install apache2 -y
service apache2 start
service apache2 status
docker p q                #to exit container
docker ps -a              #to list all containers
docker attach cont_name   #to go inside container
docker stop cont_name     #to stop container
docker start cont_name    #to start container
docker pause cont_name    #to pause container
docker unpause cont_name  #to unpause container
docker inspect cont_name  #to get complete info of a container
docker rm cont_name       #to delete a container
STOP       #will wait to finish all process running inside container
KILL       #won’t wait to finish all process running inside container
```

## **OS LEVEL OFVIRTUALIZATION:**

```bash
docker pull ubuntu
docker run -it --name container1 ubuntu
apt update -y
apt install mysql-server apache2 python3 -y
touch file{1..5}
apache -v
mysql-server --version
python3 --version
ls
ctrl p q
docker commit container1 saim:v1
docker run -it --name container saim:v2
apache -v
mysql-server -version
python3 --version
ls
```

## **DOCKERFILE:**
It is an Automation way to create Image.                                  
Here we use Components to create Image.                                     
In Dockerfile D must be Capital.                                           
Components also capital.                                                  
This Dockerfile will be Reusable.                                          
Here we can create image directly without container help.                  
Name: Dockerfile 
```bash
docker kill $(docker ps -qa)                                               
docker rm $(docker ps -qa)     
docker rmi -f $(docker images -qa)
```
## **COMPONENTS:**
**FROM**:       used to base image                                          
**RUN**:        used to run Linux commands (During image creation)          
**CMD**:        used to run Linux commands (After container creation)       
**ENTRYPOINT**: high priority than CMD                                    
**COPY**:       to copy local files to container                            
**ADD**:        to copy internet files to container                         
**WORKDIR**:    to open required directory                                  
**LABEL**:      to add labels for Docker images                             
**ENV**:        to set environment variables (Inside Container)             
**ARGS**:       to pass environment variables (Outside Container)           
**EXPOSE**:     to give port number

EX-1:
```bash
FROM ubuntu
RUN apt update -y
RUN apt install apache2 -y
docker build -t saim:v1 .
docker run -it --name container1 saim:v1
```

EX-2:
```bash
FROM ubuntu
RUN apt update -y
RUN apt install apache2 -y
RUN apt install python3 -y
CMD apt install mysql-server -y
docker build -t saim:v2 .
docker run -it --name container2 saim:v2
```

EX-3:
```bash
FROM ubuntu
COPY index.html /tmp
ADD http://dlcdn.apache.org/tomcat/tomcat-9/v9.0.89/bin/apache-tomcat-9.0.89.tar.gz /tmp
docker build -t saim:v3 .
docker run -it --name container3 saim:v3
```

EX-4:
```bash
FROM ubuntu
COPY index.html /tmp
ADD http://dlcdn.apache.org/tomcat/tomcat-9/v9.0.89/bin/apache-tomcat-9.0.89.tar.gz /tmp
WORKDIR /tmp
LABEL author Saimhazeq
docker build -t saim:v4 .
docker run -it --name container4 saim:v4
```

EX-5:
```bash
FROM ubuntu
LABEL author Saimhazeq
ENV client swiggy
ENV server appserver
docker build -t saim:v5 .
docker run -it --name container5 saim:v5

## **APP Netflix – DEPLOYMENT**
yum install git -y
git clone https://github.com/SaimHazeq/netflix-clone.git
mv neflix-clone/*
```

## **Dockerfile**
```bash
FROM apt update
RUN apt install apache2 -y
COPY * /var/www/html/
CMD [“/usr/sbin/apachectl”, “-D”, “FOREGROUND”]
docker build -t Netflix:v1 .
docker run -it --name netflix1 -p 80:80 netflix:v1
```

## **VOLUMES:**
It is used to store data inside container.                                  
Volume is a simple directory inside container.                             
Containers uses host resources (cpu, ram, rom).                             
Single volume can be shared to multiple containers.                         
Ex: container-1 (vol1) --> container-2 (vol1) & container-3 (vol1) --> Cont4.                                                                      
At a time we can share single volume to single container only.

**METHOD-1:**
DOCKER FILE:
```bash
FROM ubuntu
Volume [“/volume1”]
docker build -t saim:v1 .
docker run -it --name container1 saim:v1
cd volume1/
touch file{1..5}
cat>file1
ctrl p q
docker run -it --name container1 --volumes-from container1 ubuntu
```
**METHOD-2:**
FROM CLI:
```bash
docker run -it --name container3 -v volume2 ubuntu
cd volume1/
touch java{1..5}
ctrl p q
docker run -it --name container4 --volumes-from container3 ubuntu
```

**METHOD-3:**
VOLUME MOUNTING:
```bash
docker volume ls : to list volumes
docker volume create name : to create volume
docker volume inspect volume3 : to get info of volume3
cd /var/lib/docker/volumes/volume3/_data
touch python{1..5}
docker run -it --name container5 --mount source=volume3,destination=/volume ubuntu
```

HOST --> CONTAINER:
```bash
cd /root
touch saim{1..5}
docker volume inspect volume4
cp * /var/lib/docker/volumes/volume4/_data
docker attach container6
ls /volume4
```

## **DOCKER SYSTEM COMMANDS:**
Used to know complete information about the docker elements.
```bash
docker system df         #to give info of docker objects
docker system df -v
docker inspect container4 | grep -i volume
docker inspect container5 | grep –I volume
docker system prune      #to remove unused objects of docker
```
## **DOCKER MEMORY MANAGEMENT:**
Containers uses our host resources (cpu, mem)                            
By default we don’t have any limits for containers                          
We need to set it
```bash
docker run -itd --name container1 --memory=”200mb” --cpus=”0.2” ubuntu
docker inspect container1
docker stats
vim Dockerfile
FROM ubuntu
RUN apt update -y
RUN apt install apache2 -y
COPY index.html /var/www/html
CMD ["/usr/sbin/apachectl", "-D", "FOREGROUND"]Index.html: take form w3 schools
docker build -t movies:v1 .
docker run -itd --name movies -p 81:80 movies:v1
docker build -t train:v1 .
docker run -itd --name train -p 82:80 train:v1
docker build -t dth:v1 .
docker run -itd --name dth -p 83:80 dth:v1
docker build -t recharge:v1 .
docker run -itd --name recharge -p 84:80 recharge:v1
docker ps -a -q : to list container id’s
docker kill $(docker ps -a -q) : to kill all containers
docker rm $(docker ps -a -q) : to remove all containers
```

NOTE: In the above process all the containers are managed and created one by one.                                                                     
In real time we manage all the containers at same time so for that purpose  we are going to use                                                        
the concept called Docker Compose.

## **DOCKER COMPOSE:**
It’s a tool used to manage multiple containers in single host.              
We can create, start, stop, and delete all containers together.             
We write container information in a file called Compose file.               
Inside the compose file we can give images, ports, and volumes info of containers.                                                                
We need to download this tool and use it.

**INSTALLATION:**
```bash
Sudo curl -L “https://github.com/docker/compose/release/download/Vesion/docker-compose-
$(uname -s)-$(uname -m)” -o /usr/local/bin/docker-compose
ls /usr/local/bin/
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose version
```
In Linux majorly you are having two type of commands first one is inbuilt commands which come with the operating system by default.                   
Second one is download commands we are going to download with the help of yum, apt, or amazon linux extras command.

Some commands we can download on binary files.

NOTE: Linux will not give some commands, so to use them we need to download separately.                                                               
Once a command is downloaded we need to move it to               /usr/local/bin because all the userexecuted commands In Linux will store in /usr/local/bin                                                              

Executable permission need to execute the command.
```bash
version: '3.8'
services:
  movies:
   image: movies:v1
   ports:
    - "81:80"
  train:
   image: train:v1
   ports:
    - "82:80"
  dth:
   image: dth:v1
   ports:
     - "83:80"
  recharge:
   image: recharge:v1
   ports:
     - "84:80"
```

**COMMANDS:**
```bash
docker-compose up -d    #to create and start all containers
docker-compose stop     #to stop all containers
docker-compose start    #to start all containers
docker-compose kill     #to kill all containers
docker-compose rm       #to delete all containers
docker-compose down     #to stop and delete all containers
docker-compose pause    #to pause all containers
docker-compose unpause  #to unpause all containers
docker-compose ps -a    #to list the containers managed by compose
file
docker-compose images   #to list the images managed by compose
file
docker-compose logs     #to show logs of docker compose
docker-compose top      #to show the process of compose containers
docker-compose restart  #to restart all the compose containers
docker-compose scale cont_name=10   #to scale the service

#CHANGING THE DEFAULT FILE
#By default the docker-compose will support the following names

docker-compose.yml, docker-compose.yaml,
compose.yml, compose.yaml
mv docker-compose.yml saim.yml
docker-compose up -d : throws an error
docker-compose -f saim.yml up -d
docker-compose -f saim.yml ps
docker-compose -f saim.yml down
```
Images we create on server.                                                
These images will work on only this server.                                 

git (local) --> github (internet) = to access by other                      
image (local) --> dockerhub (internet) = to access by others

**STEPS:**                                                                 
Create DockerHub account                                                   
Create a Repository
```bash
docker tag container_name user_name/repository_name
docker login --> username & password
docker push user_name/ repository_name

docker tag container_name user_name/ repository_name
docker push user_name/repository_name

docker tag container_name user_name/ repository_name
docker push user_name/repository_name

docker tag container_name user_name/repository_name
docker push user_name/ repository_name

docker rmi -f $(docker image –q)
docker pull user_name/repository_name:latest
```
**High Availability:** More than one server                                 
**Why**: If one server got deleted than other server will gives the app.

## **DOCKER SWARM:**
It’s an orchestration tool for containers.                                 
Used to manage multiple containers on multiple servers.                    
Here we create a cluster (group of servers).                                
In that cluster we can create same container on multiple servers.           
Here we have the manager node and worker node.                             
Manager node’s main purpose is to maintain the container.                  
Without Docker engine we can’t create the cluster.                         
Port: 2377                                                                  
Worker node will join on cluster by using a token.                          
Manager node will give the token.                                           

**SETUP:**                                                                 
Create 3 Servers                                                           
Install docker and start the service                                       
```bash
yum install docker –y
systemctl start docker
hostnamectl set-hostname Manager
hostnamectl set-hostname Worker-1
hostnamectl set-hostnamce Worker-2
#Enable 2377 port

docker swarm init (manager) --> #copy-paste the token to worker nodes.
docker node ls
```
**Note:** Individual containers are not going to replicate.                
If we create a service then only containers will be distributed. 

**Service:** It’s a way of exposing and managing multiple containers.       
In service we can create copy of containers.                                
That container copies will be distributed to all the nodes.                 
Service --> Containers --> Distributed to nodes                            

`docker service create --name container_name --replicas 3 -p 81:80
saimhazeq/container_name:latest`
```bash
docker service ls               #to list services
docker service inspect movies   #to get complete information of service
docker service ps movies        #to list the containers of movies
docker service scale movies=10  #to scale in the containers
docker service scale movies=3   #to scale out the containers
docker service rollback movies  #to go previous state
docker service logs movies      #to see the logs
docker service rm movies        #to delete all services
```
When scale down It follows LIFO pattern.                                   
LIFO = LAST-IN-FIRST-OUT 

**Note:**
If we delete a container it will recreate automatically itself.            
It is called as Self-Healing.                                               

## **CLUSTER ACTIVITIES:**
```bash
docker swarm leave (worker)        #to make node inactive from cluster
#To active the node copy the token.
docker node rm node_id (manager)   #to delete worker node which is on down state
docker node inspect node_id        #to get complete info of worker node
docker swarm join-token (manager)  #to generate the token to join
```
**Note:**
We can’t delete the node which is ready state.                              
If we want to join the node to cluster again we need to paste the token on worker node.

## **DOCKER NETWORKING:**
Docker networks are used to make communication between the multiple containers that are running on same or different docker hosts.

We have different types of docker networks. 

**1.Bridge Network :**     Same Host                                            
**2.Overlay Network :**    Different Host                                       
**3.Host Network**                                                            
**4.None Network**                                                           

**1.Bridge Network:**                                                         
It is a default network that container will communicate with each other within the same host. 

**2.Overlay Network:**                                                        
Used to communicate containers with each other across the multiple docker hosts.             

**3.Host Network:**                                                           
When you want your container IP and EC2 instance IP same then you use host network.          

**4.None Network:**                                                           
When you don’t want the container to get exposed to the world, we use none network.                                                                    
It will notprovide any network to our container.
```bash
docker network create network_name   #to create a network
docker network rm network_name       #to see the list
docker network inspect network_name  #to inspect
docker network connect network_name container_id/name
                                     #to connect a container to the network
docker exec -it container1 container_name /bin/bash
apt update
apt install iputils-ping -y          #command to install ping checks
ping ip_address of container2
docker network disconnect network_name container_name
                                    #To disconnect from the container
docker network prune : to prune
