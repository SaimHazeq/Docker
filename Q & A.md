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
**Docker achieves isolation using Linux Kernel features such as Namespaces and Control Group(cgroups).**  

**1. Namespaces: Provide isolation for processes, networking, hostnames, users, and file systems.**   

**2. cgroups: Control and limit resource usage such as CPU, memory, and disk I/O.**  

**3. Union File System: Provides separate container filesystem layers.**  

### 12. Difference between container runtime vs container engine. 
**Container engine**  
- Manages the overall container lifecycle, including building images, networking, and storage.
    
**Container runtime**
- Responsible for actually creating and running containers. For example, Docker engine uses containerd and runc to execute containers.

### 13. Difference between CMD vs ENTRYPOINT. 
**CMD**   
- Provides default commands or arguments that can be overridden when running a container.

**ENTRYPOINT**   
- Defines the main executable that runs when the container starts. It can not be overridden.

### 14. What is multi-stage build? 
**Multi-stage build is a Docker feature that allows us to use multiple `FROM` instructions in a single Dockerfile to separate the build environment from the runtime environment.**  

**It helps reduce Docker image size by including only the required application files and dependencies in the final image, excluding unnecessary build tools.**

### 15. How do you inspect a Docker image?  
**We use `docker inspect` command to view detailed information about a Docker image, including its configuration, layers, environment variables, architecture, and metadata.**

### 16. How do you scan Docker images for vulnerabilities?
**We scan Docker images for security vulnerabilities using tools like Trivy, and Docker Scout.**   
`trivy image nginx:latest`   

**It identifies vulnerabilities in OS packages, application dependencies, and libraries, categorizing them by severity (Critical, High, Medium, Low).**

### 17. Container crashes after starting — how do you debug?
** If a container crashes after starting, I first check its status using `docker ps -a`, then analyze application logs using `docker logs`.**    

**I inspect the exit code and container configuration using `docker inspect`.**  

**I also check resource limits, environment variables, dependencies, and startup commands to identify the root cause.**  

**After fixing the issue, I restart the container any verify that the application is running properly.**

### 18. Container exits immediately — why? 
**A container exits immediately when its main process finishes or crashes.**  

**I check the container status using `docker ps -a`, review logs using `docker logs`, and inspect the exit code and configuration using `docker inspect`.**   

**Then I identify whether the issue is related to the startup command, application errors, missing dependencies, or resource constraints.**

### 19. What is Docker networking and network types?  
**Docker networking allows containers to communicate with each other and external network.**  

**Docker provides 4 main network types:**  
- **Bridge: Allows containers on the same Docker host to communicate with each other.(It's a default Network)**
- **Host: Shares the host machines's network namespace.**
- **None: Disables container networking.**
- **Overlay: Enables communication between containers running on different Docker hosts.**
- **Macvlan: Assigns containers their own MAC addresses, making them appear as physical devices on the network.**
   
### 20. What is port mapping?   
**Port mapping allows us to expose a container's application to the outside world by mapping a host port to a container port.**  
  
**For example, `-p 8080:80` maps host port 8080 to container port 80.**
  
### 21. How do containers communicate with each other?  
**Container communicate with each other through Docker networks using container IP addresses or container names (DNS).**

### 22. How does Docker networking work in multi-host environments?  
**Docker uses Overlay Networking to enable communication between containers running on different Docker hosts.**   

**It creates a virtual network across multiple hosts, allowing containers to communicate securely as if they were on the same network.**

### 23. Two containers cannot communicate — how do you troubleshoot? 
**If two containers cannot communicate, I troubleshoot the Docker network, container connectivity, ports and firewall rules.**   
   
**Troubleshooting Steps**

**1. Check running containers**   
`docker ps`    
    
**2. Check network configuration**   
`docker network ls`        
`docker network inspect my-network `     
      
**3. Verify both containers are on the same network.**    
   
**4. Test connectivity**    
`docker exec container1 ping container2`    
    
**5. Check application listening ports**   
`docker exec container2 ss -tulnp`    
    
**6. Check container logs**   
`docker logs container2`     
     
**7. Verify firewall rules and network policies.**   

### 24. What is Docker Volumes Why do we need Docker Volumes?
**Docker Volumes are used to persist data generated by containers. They store data outside the container's writable layes, so data remains available even if the container is stopped, deleted, or recreated.**   

**Why Need?**  
- **Data Persistence: Prevents data loss when containers are removed.**
- **Data Sharing: Allows multiple containers to access shared data.**
- **Backup and Recovery: Makes application data easier to track back up and restore.**
- **Separation: Keeps application data separate from the container lifecycle.**

### 25. Difference between Volume vs Bind Mount. 
**Volume**  
- **Managed by Docker and are commonly used for persistent application data, especially in production.**
- **Store in Docker's storage directory.**
- **Easier to manage and backup.**
**Bind Mount**
- **Directly  map a specific host directory of file into a container and are commonly used during development to share source code or configuration files.**
- **Used a specific host filesystem path.**
- **Requires managing host paths and permissions.**

### 26. What is tmpfs mount?  
**Tmpfs Mount is a temporary storage mechanism that stores data in the host's memory (RAM) instead of disk. The data is removed when the container stops or restart.**

### 27. How do you backup Docker volumes? 
**I backup Docker volumes using a temporary container with the `tar` command. I mount the volume inside the container, compress its data into a backup archive, and store it on the host machine or external storage like Amazon S3.**    
**Example**  
  
```docker run --rm \
  -v my-volume:/data \
  -v $(pwd):/backup \
  ubuntu tar czf /backup/volume-backup.tar.gz -C /data .
```

### 28. How do you persist container data? 
**I use Docker volumes to persist application data outside the container lifecycle. This ensures data remains available even if the container is stopped, deleted, or recreated.**

### 29. My container data disappears after restart — why? 
**Container data disappears when it's stored in the container's writable layer instead of persistent storage. To prevent this, I use Docker volumes or Bind mounts to store data outside the container lifecycle. This ensures data remains available even after container restarts, deletion, or recreation.**

### 30. What is Docker Compose?  
**Docker Compose used to manage multiple containers applications. We defines services, networks, volumes, and configuration in a YAML file and use commands like `docker compose up -d` to start all containers together. It simplifies application deployment and management.**

### 31. How do you secure Docker images? 
**I secure Docker images by using trusted and minimal base images, scanning them with Trivy for vulnerabilities, avoiding hardcoded secrets, and running containers as non-root users.** 

### 32. What are Docker security risks?   
**Common Docker security risks include running containers as root, using vulnerable or untrusted images, exposing the Docker socket, hardcoding secrets, excessive container privileges, and container escape vulnerabilities.**  

**I mitigate these risks by using trusted images, scanning with Trivy, running containers as non-root users, implementing least-privilege access, and following network security best practices.**

### 33. What is container isolation? 
**Container isolation ensures the each container runs independently without interfering with other container.**  

**Docker uses namespaces to isolate processes, networking, and filesystem, while cgroups control resource usage such as CPU and memory.**

### 34. Container running as root — why is it dangerous?
**Running a container as root is dangerous because it gives the application elevated privileged inside the container. If an attacker exploits the application or escapes the container, they may gain access to the host system, especially when additional privileges or misconfiguration exist.**

### 35. How do you integrate Docker with CI/CD? 
**I integrate Docker with jenkins CI/CD pipelines to automate the entire deployment process.**  

**Whenever developers push code to GitHub, Jenkins triggers the pipeline, builds and test the application, creates a Docker image, scans it using Trivy, and pushes it to Amazon ECR.**  

**Finally, we deploy the image to Kubernetes EKS using Helm. This makes deployments faster, consistent, and reliable.**

### 36. How do you version Docker images?  
**I version Docker images using tags such as `v1.0` and `v1.1`.**  

**In CI/CD pipelines, I prefer using Git commit IDs as image tags to uniquely identify each build.**  

**I push these versioned images to Amazon ECR, which helps with deployment tracking, rollback, and release management.**

### 37. Your Docker image is 2GB — how do you reduce it?  
**If my Docker image is 2GB, I first analyze its layers using `docker history`.**  

**Then I use lightweight base images, multi-stage builds, remove unnecessary dependencies and cache files, and optimize the Dockefile.**  

**I also use `.dockerignore` to exclude unnecessary files.**  

**Finally, I rebuild and compare the image size to verify the optimization.**

### 38. Your container keeps restarting — how do you debug? 
**If a container keeps restarting, I first check its status using `docker ps -a` and analyze logs using `docker logs <container_id>`.**  

**Then I inspect the exit code `docker inspect <container_id>`, restart policy, and container configuration.**  

**I also check for application crashes, incorrect environment variables, missing dependencies, and memory issues.**  

**After identifying and fixing the root cause, I restart the container and verify its stability.**

### 39. Container cannot connect to database — how to troubleshoot? 
**If a container cannot connect to a database, I first check application logs to identify the connection error.**  

**Then I verify that both containers are on the correct network, check database hostname and port, validate credentials and environment variables, and verify firewall or security group rules.**  

**I also ensure the database is running and accepting connections. After fixing the issue, I test connectivity again and verify that the application connects successfully.**      
```  
docker ps
docker logs <container_id>
docker network inspect my-network   #verify network
nc -zv <database-host> 5432   #check database port accessibility
```

### 40. Application works locally but fails in container — why?
**If an application works locally but fails inside a container, I first check container logs to identify the error.**  

**Then I verify dependencies, environment variables, file permission, port configurations, and network connectivity.**  

**I also check runtime and OS compatibility. After identifying the root cause, I fix the Dockerfile or container configuration, rebuild the image, and test it again.**
  
### 41. Docker build takes too long — how to optimize? 
**If Docker builds take too long, I first identify which steps consume the most time.**  

**Then I optimize Dockerfile layer ordering to improve caching, use `.dockerignore` to reduce the build context, enable BuildKit, and cache dependencies.**   

**I also use multi-stage builds and lightweight base image to improve build efficiency.**

### 42. Container logs filling disk — how to solve?  
**If container logs are filling up disk space, I first identify which containers are generating excessive logs.**   

`docker inspect --format='{{.LogPath}}' <container_id>`    
    
**Then I configure Docker log rotation using `maz-size` and `max-file` to limit log storage.**   

**Update Docker's `daemon.json`**  
```
{
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "10m",
    "max-file": "3"
  }
}
```

### 43. How do you handle secrets in containers? 
**I never hardcode secrets in Dockerfile or containers images.**  

**In AWS environments, I use AWS Secrets Manager to securely store database credentials and API keys.**  

**Applications retrieve secrets at runtime using IAM roles and appropriate permissions.**  

**I also ensure secrets are not exposed in logs, source code, or CI/CD pipelines.**


### 44. How do you deploy containers in production?  
**In production, I use Jenkins CI/CD to automate container deployments. Whenever code is pushed to GitHub, Jenkins build and test the application, creates a Docker Image, scans it using Trivy, and pushes it to Amazon ECR.**  

**Then we deploy the image to Amazon EKS using Helm. I configure health checks, resource requests and limits, and auto-scaling.**    

**For monitoring, I use Prometheus and Grafana, and if a deployments fails, I perform a rollback to the previous stable version.**


### 45. How do you monitor containers?   
**I monitor Container using Prometheus and Grafana to track CPU, memory, network and application performance.**  

**I use cAdvisor to collect container-level metrics and CloudWatch for centralized logging.**  

**I also configure alerts for high resource utilization, container restarts, and application failures to identify production issues early.**


### 46. What is service discovery in Docker? 
**Service Discovery allows containers to communicate with each other using service names instead of IP addresses.**  

**Docker provides built-in DNS resolution, which automatically resolves service names to container IP addresses.**  

**This simplifies communication between container, especially when containers are recreated or their IP addresses change.**



### 47. What is image immutability?
**Image immutability means that once a Docker Image is built, it should not be modified. If any application code or dependency changes, we build a new image with a new version or tag.**  

**Why is it Important**  
- **Ensure consistent deployment across environments.**
- **Improves version control and traceability.**
- **Makes rollbacks easier.**
- **Reduces unexpected production issues.**


### 48. What are distroless images?
**Distroless images are minimal container images that contains only the application and its required runtime dependencies, without unnecessary tools like shells, package managers, or debugging utilities.**


### 49. What is init container?
**An init container is used in Kubernetes to perform startup and initialization tasks before the main application container starts.**  

**Example: We can use it to check database connectivity, download configuration files, or prepare required dependencies.**

### 50. How do you build secure production Docker images?
**I build secure production Docker images using trusted minimal base images and multi-stage builds. I run applications as non-root users, avoid hardcoding secrets, and scan images using Trivy for vulnerabilities. I also use versioned image tags, remove unnecessary dependencies, and integrate security scanning into Jenkins CI/CD pipelines before pushing images to Amazon ECR.**
