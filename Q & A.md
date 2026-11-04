### 1. What is Docker?
**Docker is an open-source containerization platform used to build, package, and run applications inside containers.**     
   
**A container includes:**   
- Application code
- Runtime
- System libraries
- Dependencies
- Configuration
**This ensures the application runs consistently across different environments such as development, testing and production.**     
      
**Before Docker, developers often faced the "it works on my machine" problem, where an application runs locally but fails in another environment due to dependency differences.**       
     
**Docker solves this by packaging the application with everything it needs.**   

### 2. What is a container?     
**A container is a lightweight, isolated environment that packages an application along with its dependencies, libraries, and runtime.**                  
     
**It ensures the application runs consistently across development, testing, and production environments.**               
            
**In Docker, containers are created from image and share the Host OS kernel, making them faster and more resource-efficient than virtual machines.**           

### 3. What is a Docker image?  
**A Docker image is a read-only template that contains application code, runtime, libraries, dependencies, and configuration required to run an application.**    

**It is used to create Docker Containers>**   

**Example: You build a Docker image for a Python application, push it to Amazon ECR, and use that image to create containers in Docker or Kubernetes.**

### 4. What is a Dockerfile? 
**A Dockerfile is a text file that contains instructions to build a Docker Image. It defines the base image, application code, dependencies, working director, ports, and startup commands.**   

### 5. What is Docker Engine?   
**Docker Engine is the core runtime that builds, runs, and manages Docker containers. It consists of the Docker daemon, REST API, and Docker CLI.**   

**It handles tasks such as pulling images, creating containers, managing networks, and handling storage volumes.**

### 6. What are the main components of Docker architecture? 
**Docker architecture has 4 main components:**  

**1. Docker Client: Allows users to interact with Docker using commands like `docker run` and `docker build`.**  

**2. Docker Daemon(dockerd): Manages Docker images, containers, networks, and volumes.**  

**3. Docker Registry: Stores and distributes Docker images, such as Docker Hub and Amazon ECR.**

**4. Docker Objects: Include images, containers, networks, and volumes.**   

**Docker follows a client-server architecture. The Docker client sends commands to the Docker daemon through the REST API. The daemon builds images, creates and manages containers, and communicates with Docker registries to pull or push images.**

### 7. What happens when you run docker run?  
**When I execute `docker run`, Docker checks for the image locally. If it's unavailable, it pulls the image from the registry, creates a container, configures its networking and filesystem, and starts the application inside the container.**

### 8. What is the Docker daemon?  
**Docker Daemon(dockerd) is a background service responsible for building, running, and managing Docker containers, images, networks, and volumes.**   

**It receives request from the Docker Client through the Docker REST API and performs the requested operations.**

### 9. What is the Docker client? 
**Docker Client is a command-line interface(CLI) that allows users to interact with Docker. It sends commands like `docker build`, `docker pull`, and `docker run` to the Docker daemon through the REST API.**

### 10.Explain Docker architecture.  
**Docker Architecture follows a client-server architecture consisting of three main components:**     
    
**1. Docker Client: Accepts user commands such as `docker build`, `docker pull` and `docker run`.**  

**2. Docker Daemon: Receives request from the client and manages images, containers, network, and volumes.**   

**3. Docker Registry: Stores images, such as Docker Hub and Amazon ECR.**  

### 11.How does Docker achieve isolation?    
Difference between container runtime vs container engine.   
Difference between CMD vs ENTRYPOINT.    
What is multi-stage build?   
How do you inspect a Docker image?    
How do you scan Docker images for vulnerabilities?    
Container crashes after starting — how do you debug?   
Container exits immediately — why?     
What is Docker networking?  
What are Docker network types?   
Difference between bridge, host, overlay, macvlan networks.   
What is the default network in Docker?   
What is port mapping?   
How do containers communicate with each other?   
How does Docker networking work in multi-host environments?   
Two containers cannot communicate — how do you troubleshoot?   
Why do we need Docker volumes?   
Difference between Volume vs Bind Mount.    
What is tmpfs mount?   
How do you backup Docker volumes?   
How do you persist container data?   
My container data disappears after restart — why?    
What is Docker Compose?   
How do you secure Docker images?   
What are Docker security risks?   
What is container isolation?   
Container running as root — why is it dangerous?    
How do you integrate Docker with CI/CD?   
How do you version Docker images?   
Your Docker image is 2GB — how do you reduce it?   
Your container keeps restarting — how do you debug?   
You need to run 100 containers — how do you manage them?   
Container cannot connect to database — how to troubleshoot?  
Application works locally but fails in container — why?   
Docker build takes too long — how to optimize?   
Container logs filling disk — how to solve?    
How do you handle secrets in containers?   
How do you deploy containers in production?   
How do you monitor containers?   
What is Docker Swarm?    
What is service discovery in Docker?    
What is image immutability?   
What are distroless images?   
What is init container?   
How do you build secure production Docker images?    
