# Docker --> Build --> ship --> Run



# 🐳 Docker Commands - DevOps Quick Guide

Welcome to the **Docker Commands Handbook** 🚀  
This guide covers all essential Docker commands organized like an index for quick reference.

---

# 📑 Table of Contents

1. 📦 Images  
2. 🚀 Containers  
3. 🔍 Debugging & Logs  
4. 🧱 Dockerfile & Image Build  
5. 🌐 Networking  
6. 💾 Volumes (Data Persistence)  
7. 🧹 Cleanup  

---

# 📦 1. Images

- `docker images` → List images  
- `docker pull <image>` → Download image  
- `docker rmi <image>` → Remove image  
- `docker build -t <name>:<tag> .` → Build image  

---

# 🚀 2. Containers

- `docker run -d -p 8080:80 nginx` → Run container  
- `docker ps` → Running containers  
- `docker ps -a` → All containers  
- `docker stop <id>` → Stop container  
- `docker start <id>` → Start container  
- `docker rm <id>` → Remove container  

---

# 🔍 3. Debugging & Logs

- `docker logs <id>` → View logs  
- `docker exec -it <id> /bin/bash` → Access container  
- `docker inspect <id>` → Detailed info  

---

# 🧱 4. Dockerfile & Image Build

- `docker build -t myapp:v1 .` → Build image  
- `docker tag myapp:v1 repo/myapp:v1` → Tag image  
- `docker push repo/myapp:v1` → Push image  

---

# 🌐 5. Networking

- `docker network ls` → List networks  
- `docker network create mynetwork` → Create network  
- `docker run --network=mynetwork nginx` → Use network  
- `docker network inspect mynetwork` → Inspect network  

---

# 💾 6. Volumes

- `docker volume create myvolume` → Create volume  
- `docker run -v myvolume:/data nginx` → Use volume  
- `docker volume ls` → List volumes  
- `docker volume rm myvolume` → Remove volume  

---

# 🧹 7. Cleanup

- `docker container prune` → Remove stopped containers  
- `docker image prune` → Remove unused images  
- `docker system prune -a` → Clean everything ⚠️  

---

# 🔄 Docker Lifecycle

**Build → Ship → Run**

```bash
docker build -t myapp:v1 .
docker push repo/myapp:v1
docker run -d -p 8080:80 myapp:v1
