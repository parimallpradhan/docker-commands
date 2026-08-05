# 🧱 Dockerfile & Image Build Commands


## Simple Dockerfile (Ubuntu + Git + Java)

```dockerfile
# Base Image
FROM ubuntu:24.04

# Install Git and Java
RUN apt-get update && \
    apt-get install -y git openjdk-21-jdk

# Default command
CMD ["/bin/bash"]
```

### Build

```bash
docker build -t myimage:v1 .
```

### Run

```bash
docker run -it --name c1 myimage:v1
```

### Verify

```bash
git --version
```

```bash
java -version
```

---

```dockerfile
FROM ubuntu:24.04     # Base Image

RUN apt-get update && \
    apt-get install -y git openjdk-21-jdk   # Install software

CMD ["/bin/bash"]     # Start Bash when the container runs
```



---

## 🏗️ 1. Build Image

```bash id="k8f3pz"
docker build -t myapp:v1 .
```

👉 Builds Docker image from a Dockerfile
👉 `-t` = tag (name:version)
👉 `.` = current directory (Dockerfile location)

✅ **Example:**

```bash id="x1p9vb"
docker build -t ecommerce-app:v1 .
```

👉 Builds image for your application

---

## 🏷️ 2. Tag Image

```bash id="q4z8rm"
docker tag myapp:v1 myrepo/myapp:v1
```

👉 Adds a new tag (rename for registry)

✅ **Example:**

```bash id="n6t2wy"
docker tag ecommerce-app:v1 mydockerhub123/ecommerce-app:v1
```

👉 Prepare image for Docker Hub push

---

## 📤 3. Push Image

```bash id="m2c7df"
docker push myrepo/myapp:v1
```

👉 Uploads image to Docker Hub / private registry

✅ **Example:**

```bash id="b9r5kx"
docker push mydockerhub123/ecommerce-app:v1
```

👉 Push image for CI/CD deployment

---

# 🔄 Complete Flow (Very Important)

```bash id="y8w4nt"
docker build -t myapp:v1 .
docker tag myapp:v1 myrepo/myapp:v1
docker push myrepo/myapp:v1
```

👉 **Build → Tag → Push = CI/CD pipeline flow**

---

# 🧪 Hands-On Lab

---

## 🎯 Step 1: Create Dockerfile

```dockerfile id="d3k7qm"
FROM nginx
COPY . /usr/share/nginx/html
```

---

## 🎯 Step 2: Build Image

```bash id="p6v9js"
docker build -t myweb:v1 .
```

---

## 🎯 Step 3: Run Container

```bash id="u2x8qa"
docker run -d -p 8080:80 myweb:v1
```

👉 Open: `http://localhost:8080`

---

## 🎯 Step 4: Push to Docker Hub

```bash id="h5m1zl"
docker login
docker tag myweb:v1 myrepo/myweb:v1
docker push myrepo/myweb:v1
```

---

# 🧠 DevOps Tips

👉 Always use version tags (`v1`, `v2`)
👉 Avoid `latest` in production ❌
👉 Keep Dockerfile optimized (small image size) ⚡

---

# ⚡ One-Line Summary

👉 **Dockerfile → Build → Tag → Push = Application delivery pipeline**

---

