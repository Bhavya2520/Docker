# 🐳 Dockerfile Creation using Dockerfile

## 📄 What is Dockerfile?
- Dockerfile is a **text file** that contains a set of **instructions**.
- It is used for the **automation of Docker image creation**.

---

## 🧱 Basic Dockerfile Instructions

### 🔹 `FROM`
- Sets the **base image**.
- This **must be the first instruction** in the Dockerfile.

### 🔹 `RUN`
- Executes commands and **creates a new layer** in the image.

### 🔹 `MAINTAINER`
- Specifies the **author or owner** of the image.
- *(Note: Deprecated in favor of LABEL)*

### 🔹 `COPY`
- Copies files from the **local system** (Docker host) into the image.
- Syntax: `COPY <source> <destination>`
- **Cannot download** files from the internet.

### 🔹 `ADD`
- Works like `COPY`, but with extra features:
  - Can **download files from the internet**.
  - Can **extract compressed files** (e.g., `.tar`).

### 🔹 `EXPOSE`
- Informs Docker which **port the container will listen on** at runtime.
- Example: `EXPOSE 80` (for Nginx), `EXPOSE 8080` (for Tomcat)

### 🔹 `WORKDIR`
- Sets the **working directory** inside the container.

### 🔹 `CMD`
- Defines the **default command to run** when the container starts.
- **Executed at runtime** during container creation.

### 🔹 `ENTRYPOINT`
- Similar to `CMD`, but has **higher priority**.
- The command specified in `ENTRYPOINT` **always runs first**.

### 🔹 `ENV`
- Sets **environment variables**.
- These variables are available **inside the container** at runtime.

### 🔹 `ARG`
- Defines **build-time variables**.
- Difference from `ENV`:
  - `ARG` is used **during image build** and **not available** after the image is built.
  - `ENV` variables persist into the running container.

---

# 🐳 Creation of Dockerfile

## ✅ Steps to Create and Use a Dockerfile

1. **Create a file named `Dockerfile`**
2. **Add instructions** in the `Dockerfile`
3. **Build** the Dockerfile to create an image
4. **Run** the image to create a container

---

## 🔧 To Create an Image from a Dockerfile

```bash
docker build -t <image-name> .
```

> `-t <image-name>`: Tags the image with a name  
> `.`: Refers to the current directory (context)

---

## 🧪 Check Process State

```bash
docker ps -a
```

> Shows all containers (running and stopped)

---

## 📦 See Docker Images

```bash
docker images
```

> Lists all locally stored Docker images

---

## 🚀 To Create a Container from an Image

```bash
docker run -it --name <container-name> <image-name> /bin/bash
```

- `-it`: Interactive terminal mode
- `--name`: Assigns a name to the container
- `/bin/bash`: Opens a shell inside the container


