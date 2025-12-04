# #️⃣ **5. DOCKER — COMPLETE NOTES**

---

# 🧠 **5.1 What is Docker? (Simple Explanation)**

Docker is a:

* **Containerization platform**
* Packages an application + libraries + dependencies
* Runs the same everywhere
* Lightweight (uses host OS kernel)
* Fast to start (milliseconds)

---

# 🏗 **5.2 Virtual Machine vs Container (Diagram)**

## ❌ Traditional Virtual Machines

```
+------------------------+
|    Guest OS (Ubuntu)   |
+------------------------+
|    Application         |
+------------------------+
|    Hypervisor          |
+------------------------+
|    Host OS             |
+------------------------+
|    Hardware            |
```

## ✔ Docker Containers

```
+------------------------+
| Application + Libs     |
+------------------------+
| Docker Engine          |
+------------------------+
| Host OS                |
+------------------------+
| Hardware               |
```

**Conclusion:**
Containers share the host OS → faster, lighter, more efficient.

---

# 🌳 **5.3 Docker Architecture (Diagram)**

```
          +------------------------+
          |     Docker CLI         |
          +------------+-----------+
                       |
                       v
          +------------------------+
          |     Docker Engine      |
          |   - Docker Daemon      |
          |   - REST API           |
          +------------+-----------+
                       |
                       v
          +------------------------+
          |  Container Runtime     |
          | (containerd / runc )   |
          +------------------------+
                       |
                       v
          +------------------------+
          |      Containers        |
          +------------------------+
```

---

# 📦 **5.4 Docker Key Components**

### ✔ 1. **Images**

* Read-only blueprints
* Created from a **Dockerfile**

### ✔ 2. **Containers**

* Running instances of images

### ✔ 3. **Dockerfile**

* Instructions to build an image

### ✔ 4. **Docker Hub / Registry**

* Stores Docker images

### ✔ 5. **Volumes**

* Persistent storage

### ✔ 6. **Networks**

* Communication between containers

---

# 🔁 **5.5 Docker Lifecycle Diagram**

```
Dockerfile
   ↓
docker build
   ↓
Image
   ↓
docker run
   ↓
Container
```

---

# 🧱 **5.6 Dockerfile (Complete Example)**

Create a file named **Dockerfile**:

```dockerfile
# Base image
FROM python:3.9-slim

# Set working directory
WORKDIR /app

# Copy source code
COPY . /app

# Install dependencies
RUN pip install -r requirements.txt

# Expose port
EXPOSE 5000

# Start the application
CMD ["python", "app.py"]
```

Build the image:

```bash
docker build -t myapp:v1 .
```

Run container:

```bash
docker run -d -p 5000:5000 myapp:v1
```

---

# 🧩 **5.7 Docker Compose (Multi-container Example)**

File: **docker-compose.yml**

```yaml
version: '3'
services:

  app:
    image: myapp:v1
    ports:
      - "5000:5000"
    depends_on:
      - db

  db:
    image: mysql:8
    environment:
      MYSQL_ROOT_PASSWORD: password
```

Run everything:

```bash
docker-compose up -d
```

Stop:

```bash
docker-compose down
```

---

# 🌐 **5.8 Docker Networks (Commands)**

### Create network

```bash
docker network create mynet
```

### Run container in network

```bash
docker run -d --net=mynet --name=db mysql:8
```

---

# 💾 **5.9 Docker Volumes**

### Create volume

```bash
docker volume create data_vol
```

### Use volume

```bash
docker run -v data_vol:/var/lib/mysql mysql:8
```

---

# 🧪 **5.10 MUST-KNOW DOCKER COMMANDS (with explanation + output)**

---

## ✔ Images

### List images

```bash
docker images
```

### Remove image

```bash
docker rmi <image>
```

---

## ✔ Containers

### Run container

```bash
docker run -d -p 8080:80 nginx
```

### List containers

```bash
docker ps
```

### Stop container

```bash
docker stop <id>
```

### Remove container

```bash
docker rm <id>
```

---

## ✔ Logs

```bash
docker logs <id>
```

Follow logs:

```bash
docker logs -f <id>
```

---

## ✔ Exec (Enter inside container)

```bash
docker exec -it <container> bash
```

---

## ✔ Build image

```bash
docker build -t myapp:v1 .
```

---

## ✔ Tag + Push to DockerHub

```bash
docker tag myapp:v1 myuser/myapp:v1
docker push myuser/myapp:v1
```

---

# 🔍 **5.11 CMD vs ENTRYPOINT (Simple Explanation)**

### CMD

Default command that can be overridden by `docker run`.

### ENTRYPOINT

Always runs **as main executable**.

### Recommended pattern:

```dockerfile
ENTRYPOINT ["python", "app.py"]
CMD ["--port=5000"]
```

---

# 🔀 **5.12 Docker Storage Types**

| Type       | Use Case        |
| ---------- | --------------- |
| Volume     | Persistent data |
| Bind Mount | Use host folder |
| Tmpfs      | In-memory data  |

---

# 🛡 **5.13 Docker Security Basics**

* Never run container as root
* Use small images (alpine)
* Use `.dockerignore`
* Scan image with Trivy

---

# 📝 **5.14 10 Docker Interview Questions (With Simple Answers)**

---

## **Q1. What is Docker and why use it?**

Docker is a containerization tool that:

* packages apps with dependencies
* ensures same environment everywhere
* speeds up deployments

---

## **Q2. Difference between image and container?**

| Image                   | Container          |
| ----------------------- | ------------------ |
| Blueprint               | Running instance   |
| Read-only               | Writable layer     |
| Created from Dockerfile | Created from image |

---

## **Q3. How do you build a Docker image?**

```bash
docker build -t myapp:v1 .
```

---

## **Q4. What is docker run used for?**

It starts a container:

```bash
docker run -d -p 8080:80 nginx
```

---

## **Q5. What is Docker Compose?**

Used for multi-container applications (e.g., app + db).

---

## **Q6. How to create a Docker network?**

```bash
docker network create mynet
```

---

## **Q7. How to push an image to DockerHub?**

```bash
docker push myuser/myapp:v1
```

---

## **Q8. How do you mount a volume?**

```bash
docker run -v myvol:/data mysql
```

---

## **Q9. Difference between CMD and ENTRYPOINT?**

CMD = overridable
ENTRYPOINT = always runs

---

## **Q10. How to view logs of container?**

```bash
docker logs -f <container>
```

---
