
# 🧠 **Java WAR-based application** using Dockerfile

👉 Use **Tomcat as base image**
👉 Copy WAR file
👉 Run app inside container

---

# 🐳 Dockerfile 

```dockerfile
# Step 1: Use Tomcat as base image
FROM tomcat:9

# Step 2: Remove default apps (optional but good practice)
RUN rm -rf /usr/local/tomcat/webapps/*

# Step 3: Copy WAR file into Tomcat
COPY target/*.war /usr/local/tomcat/webapps/ecommerce-app.war

# Step 4: Expose port
EXPOSE 8080

# Step 5: Start Tomcat
CMD ["catalina.sh", "run"]
```

---


## 🧱 Step-by-step explanation:

### 🔹 1. FROM

> “We are not installing Java manually — Tomcat image already has Java + server”

---

### 🔹 2. RUN

> “Cleaning default apps to avoid confusion”

---

### 🔹 3. COPY

> “Take WAR file from our project → put inside container”

---

### 🔹 4. EXPOSE

> “Container will run on port 8080”

---

### 🔹 5. CMD

> “Start Tomcat server”

---

# 🚀 Build & Run 

```bash
# Build image
docker build -t manual-app:v1 .

# Run container
docker run -p 8080:8080 manual-app:v1
```

👉 Open:

```
http://localhost:8080/app
```

---

# ☁️ Push to Docker Hub 

```bash
docker tag manual-app:v1 yourdockerhub/manual-app:v1
docker push yourdockerhub/manual-app:v1
```

---

# 🧱 Docker Compose (Final Step)

```yaml
version: "3"

services:
  app:
    image: yourdockerhub/manual-app:v1
    ports:
      - "8080:8080"
```

---



Ask students:

👉 “What happens if I change code?”



* Build new version → `v2`
* Push → QA pulls new version

---



