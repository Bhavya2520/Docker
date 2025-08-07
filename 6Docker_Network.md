# 🌐 Docker Network

## 🤔 How do Containers Talk to Each Other?

- Docker provides built-in **networking** so that containers can **communicate with each other**.
- By default, containers on the **same network** can talk to each other using **container names** as hostnames.
- Docker also ensures **strong isolation** between containers and the host system.

---

## 🔌 Types of Docker Networks

1. **Bridge** (default)
2. **Host**
3. **Macvlan**
4. **Ipvlan**
5. **Overlay**

---

## 🧱 Bridge Network (Default)

- **Most commonly used** network driver.
- Docker creates a **private internal network** on the host.
- Containers connected to this network can **communicate with each other**.
- Each container gets its **own IP address**.
- **NAT (Network Address Translation)** is used to allow outbound internet access.

### 🔹 Use Case:
> When you want **containers to talk internally**, but also want **some isolation** from the host.

### 🔧 Example:
```bash
docker network create --driver bridge my_bridge_net
```

---

## 🖥️ Host Network

- Removes network isolation between the **container** and the **host**.
- The container **shares the host's IP address and network stack**.
- No virtual network interface or NAT — it uses the **host’s ports directly**.

### 🔹 Use Case:
> Useful when you want the **highest network performance**, or when apps **must use host ports**, like some monitoring tools or VPNs.

### ⚠️ Limitation:
> No port mapping (`-p` flag has no effect) — because the container uses the host’s network directly.

### 🔧 Example:
```bash
docker run --network host nginx
```

---

> 💡 Choose the right network type based on **security**, **performance**, and **communication needs** between containers.
