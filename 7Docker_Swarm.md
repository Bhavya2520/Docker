# Docker Swarm

Docker Swarm is Docker’s native clustering and orchestration tool that lets you manage multiple Docker hosts (nodes) as a single virtual Docker engine.

Instead of running containers only on one machine, Docker Swarm enables you to scale services across multiple machines while still using the same Docker CLI and API you’re already familiar with.

---

## Why Docker Swarm Came Into the Picture

Before orchestration tools, running containers in production was tricky:

- **Scaling issues** – Running more than a few containers meant manually starting/stopping them across servers.
- **High availability** – If a container or host went down, there was no built-in mechanism to restart it automatically elsewhere.
- **Load balancing** – Distributing traffic across containers required external tools.
- **Multi-host networking** – Containers on different machines couldn’t easily talk to each other without complex networking setup.
- **Centralized management** – Teams wanted a single point to deploy, monitor, and manage containers instead of SSH-ing into multiple machines.

---

## What Docker Swarm Provides

- **Clustering** – Combines multiple Docker nodes into one logical unit.
- **Service management** – Deploy, scale, and update containers easily.
- **Load balancing** – Built-in routing mesh distributes traffic across containers.
- **Self-healing** – Automatically restarts failed containers or reschedules them on healthy nodes.
- **Rolling updates** – Update services with zero downtime.
- **Docker-native CLI/API** – Works with the same Docker commands you already know (`docker service`, `docker stack`).

---

> 💡 **In short**:  
> Docker Swarm was introduced to make containerized applications scalable, fault-tolerant, and easier to manage in production without needing to learn a completely new tool.


# 🚀 Docker Swarm Setup Guide

## 1️⃣ Pre-requirements

- Install **Docker CE** on at least **two machines** (can be physical machines, VMs, or EC2 instances).
- Enable **Docker Swarm mode** on the **manager node**.
- Ensure machines can communicate over the following **TCP ports**:

  | Port | Purpose               |
  |------|------------------------|
  | 2377 | Cluster management     |
  | 7946 | Node communication     |
  | 4789 | Overlay networking     |

---

## 2️⃣ Initialize the Swarm

Run this on the **first node** (this will be the **manager node**):

```bash
docker swarm init --advertise-addr <MANAGER-IP>
Example:

bash
Copy
Edit
docker swarm init --advertise-addr 192.168.1.100
This command will output a docker swarm join command — copy it, you’ll use it for worker nodes.

3️⃣ Join Worker Nodes to the Swarm
On each worker node, run the join command you got from Step 2:

bash
Copy
Edit
docker swarm join --token SWMTKN-1-xyz123abc... 192.168.1.100:2377
192.168.1.100 is your manager IP address.

4️⃣ Swarm Status Commands
Command	Purpose
docker node ls	Lists all nodes in the swarm (manager only)
docker info	Shows if the node is part of a swarm and its role
docker swarm inspect	Displays details of the swarm configuration
docker swarm join-token manager	Shows token to add a manager node
docker swarm join-token worker	Shows token to add a worker node

Example:

bash
Copy
Edit
docker node ls
5️⃣ Deploy a Service in Swarm
A service in Swarm is like a running application that can scale across nodes.

Example: Create an nginx service with 3 replicas:

bash
Copy
Edit
docker service create --name myweb --replicas 3 -p 8080:80 nginx
6️⃣ Service Management Commands
Command	Purpose
docker service ls	List all services in the swarm
docker service ps <service-name>	Show running tasks/containers for a service
docker service scale myweb=5	Scale a service to 5 replicas
docker service rm myweb	Remove the service

Example:

bash
Copy
Edit
docker service ls
docker service ps myweb
7️⃣ Inspect Service / Node
bash
Copy
Edit
docker service inspect myweb
docker node inspect <node-id>
8️⃣ Remove Nodes or Leave Swarm
On a worker node:

bash
Copy
Edit
docker swarm leave
On a manager node:

bash
Copy
Edit
docker swarm leave --force
vbnet
Copy
Edit
