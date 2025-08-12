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


# Docker Swarm Setup & Commands

## 1️⃣ Pre-requirements
- Install **Docker CE** on at least **two machines** (can be physical machines, VMs, or EC2 instances).
- Enable **Docker Swarm mode** on the **manager node**.
- Ensure the machines can communicate over TCP ports:
  - **2377** → Cluster management
  - **7946** → Node communication
  - **4789** → Overlay networking

---

## 2️⃣ Initialize the Swarm
Run this on the **first node** (manager node):

```bash
docker swarm init --advertise-addr <MANAGER-IP>
```

**Example:**
```bash
docker swarm init --advertise-addr 192.168.1.100
```
This will output a `docker swarm join` command — copy it for worker nodes.

---

## 3️⃣ Join Worker Nodes to the Swarm
On the **worker node(s)**, run the join command from Step 2:

```bash
docker swarm join --token SWMTKN-1-xyz123abc... 192.168.1.100:2377
```
> `192.168.1.100` is your **manager IP**.

---

## 4️⃣ Swarm Status Commands

| Command | Purpose |
|---------|---------|
| `docker node ls` | Lists all nodes in the swarm (manager only) |
| `docker info` | Shows if a node is part of a swarm and its role |
| `docker swarm inspect` | Shows details of the swarm configuration |
| `docker swarm join-token manager` | Shows the token to add another manager |
| `docker swarm join-token worker` | Shows the token to add another worker |

**Example:**
```bash
docker node ls
```

---

## 5️⃣ Deploy a Service in Swarm
A **service** in Swarm is like a running application that can scale across nodes.

**Example:** Create an nginx service with 3 replicas:
```bash
docker service create --name myweb --replicas 3 -p 8080:80 nginx
```

---

## 6️⃣ Service Management Commands

| Command | Purpose |
|---------|---------|
| `docker service ls` | List all services in the swarm |
| `docker service ps <service-name>` | Show tasks/containers running for a service |
| `docker service scale myweb=5` | Scale a service to 5 replicas |
| `docker service rm myweb` | Remove a service |

**Example:**
```bash
docker service ls
docker service ps myweb
```

---

## 7️⃣ Inspect Service/Node
```bash
docker service inspect myweb
docker node inspect <node-id>
```

---

## 8️⃣ Remove Nodes or Leave Swarm
On a **worker node**:
```bash
docker swarm leave
```
On a **manager node**:
```bash
docker swarm leave --force
```

---

## ✅ Suggested Practice Flow (Internship Task)
1. Initialize Swarm on one node.
2. Join at least **1 worker node**.
3. Check `docker node ls` and `docker swarm inspect`.
4. Create a service and list it.
5. Scale the service and check replicas with `docker service ps`.
6. Remove the service and nodes.
