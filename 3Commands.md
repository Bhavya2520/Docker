# Docker Commands

## 📦 To see all images present in your local:

```bash
docker images
```

## 🔍 To find out images in the Docker Hub:

```bash
docker search <image_name>
```

## ⬇️ To download an image from Docker Hub to a local machine:

```bash
docker pull <image_name>
```

## 🆔 To give a name to the container and run:

```bash
docker run -it --name <container_name> <image_name> /bin/bash
# [-it -> interactive mode and direct to terminal]
```

## ✅ To check whether the Docker service is running:

```bash
service docker status
```

or

```bash
service docker info
```

## ▶️ To start the Docker service:

```bash
service docker start
```

---

# Creating and Managing Containers

## 🛠️ Create a container from an image:

```bash
docker run -it --name <container_name> <update_image_name> /bin/bash
# --> ls --> cd tmp --> lso/p --> myfile [You will get all files back]
```

---

# Dockerfile Creation

## 🏗️ Docker image creation using an existing Dockerfile

### Create a container from an image:

```bash
docker run -it --name <container_name> <image_name> /bin/bash
```

### Inside container: navigate and create a file

```bash
cd tmp/
touch myfile
```

### 🔍 See the difference between base image & modified container:

```bash
docker diff <old_container_name>
# [D -> Deletion, C -> Change, A -> Append/Addition]
```

### 📸 Create a new image from a modified container:

```bash
docker commit <container_name> <container_image_name>
docker images
```

---

# Container Operations

## ▶️ Start the container:

```bash
docker start <container_name>
```

## ⏹️ Stop the container:

```bash
docker stop <container_name>
```

## 🔁 Attach to a running container:

```bash
docker attach <container_name>
```

## 📋 See all containers (running + stopped):

```bash
docker ps -a
```

## ▶️ See only running containers:

```bash
docker ps
```

## ❌ Delete a container:

```bash
docker rm <container_name>
```

## 🚪 Exit from the Docker container:

```bash
exit
```

## 🗑️ Delete an image:

```bash
docker image rm <image_name>
```
