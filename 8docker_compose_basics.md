# Docker Compose Basics – Internship Task Guide

## 1️⃣ What is Docker Compose?

Docker Compose is a **tool** that lets you define and run **multi-container Docker applications** using a single **YAML file** (usually named `docker-compose.yml`).

Instead of typing long `docker run` commands for each container, you **write your app’s services, networks, and volumes in a YAML file** and start them all at once using:

```bash
docker-compose up
```

---

### Why Docker Compose is used
- **Multiple containers at once** → Run app + database + cache, etc.
- **Simple configuration** → One file defines everything.
- **Portable** → Just share the `docker-compose.yml`, and others can run your setup.
- **Reproducible environments** → Works the same on your machine, server, or teammate’s PC.

---

## 2️⃣ The YAML file structure
Basic `docker-compose.yml` format:

```yaml
version: '3.8'  # Compose file version
services:       # All containers (services) go here
  servicename:  # Name of the container
    image:      # Docker image to use
    build:      # OR build from Dockerfile
    ports:      # Map ports: host:container
    environment: # Environment variables
    volumes:    # Mount volumes
    depends_on: # Wait for another service to start
```

---

## 3️⃣ First Example – Nginx Web Server
```yaml
version: '3.8'
services:
  web:
    image: nginx:latest
    ports:
      - "8080:80"
```

Run:
```bash
docker-compose up
```

Visit: **http://localhost:8080**

---

## 4️⃣ Example – Node + MongoDB REST API
```yaml
version: '3.8'
services:
  api:
    build: ./backend       # Folder containing Dockerfile for Node app
    ports:
      - "5000:5000"
    environment:
      - MONGO_URL=mongodb://mongo:27017/mydb
    depends_on:
      - mongo

  mongo:
    image: mongo:latest
    ports:
      - "27017:27017"
```

Here:
- `api` is your **Node.js backend**
- `mongo` is your **database**
- `depends_on` ensures Mongo starts before the API

---

## 5️⃣ Example – React App
```yaml
version: '3.8'
services:
  frontend:
    build: ./frontend  # React project folder with Dockerfile
    ports:
      - "3000:3000"
```

---

## 6️⃣ Example – PHP Laravel with MySQL
```yaml
version: '3.8'
services:
  app:
    build: ./laravel
    ports:
      - "8000:8000"
    volumes:
      - ./laravel:/var/www/html
    depends_on:
      - db

  db:
    image: mysql:5.7
    ports:
      - "3306:3306"
    environment:
      MYSQL_DATABASE: laravel
      MYSQL_ROOT_PASSWORD: root
```

---

## 7️⃣ Common Commands
| Command | Purpose |
|---------|---------|
| `docker-compose up` | Start services |
| `docker-compose up -d` | Start in background |
| `docker-compose down` | Stop and remove containers |
| `docker-compose ps` | List running services |
| `docker-compose logs` | View logs |
| `docker-compose build` | Build images |

---

## ✅ How to Complete the Internship Task
1. Learn YAML basics (spacing matters — 2 spaces for indentation).
2. Create separate folders for:
   - **Databases** (e.g., MySQL, MongoDB)
   - **Node.js REST API**
   - **React app**
   - **Laravel app**
3. Write a `docker-compose.yml` for each project.
4. Run `docker-compose up` and test.

---
