## Architecture of Docker
<img width="1009" height="527" alt="image" src="https://github.com/user-attachments/assets/f80ce38d-ee7d-4ac3-9bce-5569a0979760" />

### Docker Host  
**Docker Host** = a machine in which we are installing Docker daemon. It can be:  
- Laptop  
- Server  
- VM in your data center  
- A cloud service provider  

---

### Docker Engine / Daemon  
**How you can convert your normal system into the host:**  
- Runs on the **Host OS**  
- Responsible for running containers and managing Docker services  
- Docker daemons can communicate with other daemons  

---

### Docker CLI  
- It is the **same across all operating systems** (Windows or Linux)  
- The **same commands** are used on all OS  

---

### Docker Registries  
Example: [hub.docker.com](https://hub.docker.com)  

Docker registry **manages and stores Docker images**.  
There are two types of registries in Docker:  
1. **Public Registry**  
   - Also called **Docker Hub**  
   - Hosts public Docker images  
2. **Private Registry**  
   - Used to **share images within an enterprise**

---

### Docker Images  
- Docker images are **read-only binary templates** used to create Docker containers  
- A single file with all **dependencies and configurations** required to run a program  

---

**Ways to create a Docker image:**  
1. Take an image from Docker Hub  
2. Create an image from a Dockerfile  
3. Create an image from existing Docker containers  

---

