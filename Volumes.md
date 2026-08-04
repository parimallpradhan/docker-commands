# 💾 6. Volumes (Data Persistence)


# 🐳 Docker Volumes with Tomcat – Persistent Deployment Guide

---

## 🧩 Problem Statement

### ❌ Without Docker Volume

When you deploy a WAR file inside a Tomcat container, it is stored **inside the container filesystem**.

### 🚀 Run Tomcat Container

```bash
docker run -d -p 8080:8080 --name tomcat1 tomcat
```

### 📦 Deploy WAR File

```bash
docker cp target/ecommerce-app.war tomcat1:/usr/local/tomcat/webapps/

```

### 🌐 Access Application

```
http://localhost:8080/ecommerce-app
```

---

### 🚨 Problem

If the container is removed:

```bash
docker rm -f tomcat1
```

💥 The deployed application is **lost**

### ❗ Reason

* Containers are **ephemeral**
* Data inside container is **not persistent**
* WAR file stored inside container → deleted with container

---

## 💡 Solution: Docker Volume

Docker Volumes store data **outside the container**, ensuring persistence.

---

## ✅ Step 1: Create Volume

```bash
docker volume create tomcat-data
```

---

## ✅ Step 2: Run Tomcat with Volume

```bash
docker run -d \
  -p 8080:8080 \
  --name tomcat1 \
  -v tomcat-data:/usr/local/tomcat/webapps \
  tomcat
```

---

## ✅ Step 3: Deploy WAR File

```bash
docker cp ecommerce-app.war tomcat1:/usr/local/tomcat/webapps/
```

---

## 🔁 Step 4: Test Persistence

### Remove container

```bash
docker rm -f tomcat1
```

### Recreate container using same volume

```bash
docker run -d \
  -p 8080:8080 \
  --name tomcat2 \
  -v tomcat-data:/usr/local/tomcat/webapps \
  tomcat
```

### 🌐 Access Application Again

```
http://localhost:8080/ecommerce-app
```

✅ Application is still available

---

## 🎯 Key Concept

> Docker volumes persist data beyond the lifecycle of containers.

---

## 🔥 Real DevOps Use Case

* Jenkins builds WAR file
* CI/CD pipeline deploys to Tomcat
* Volume ensures:

  * No data loss
  * Faster recovery
  * No redeployment needed after restart

---

## 🧪 Bonus: Bind Mount (Development)

```bash
docker run -d \
  -p 8080:8080 \
  --name tomcat-dev \
  -v $(pwd)/webapps:/usr/local/tomcat/webapps \
  tomcat
```

👉 Drop WAR file into local folder → auto deployed

---

## 📊 Volume vs Bind Mount

| Feature     | Volume     | Bind Mount       |
| ----------- | ---------- | ---------------- |
| Managed by  | Docker     | User (host path) |
| Portability | High       | Low              |
| Use Case    | Production | Development      |

---

## ✅ Summary

* ❌ Without Volume → Application lost
* ✅ With Volume → Application persists
* 🚀 Best practice for real-world deployments

---

## 🏁 Conclusion

Using Docker Volumes with Tomcat ensures that your application deployments are **reliable, persistent, and production-ready**.

---


---

## 🔹 Create Volume

```bash
docker volume create myvolume
```

👉 Creates a persistent storage volume
👉 Managed by Docker (stored outside container)

✅ **Example:**

```bash
docker volume create ecommerce-data
```

---

## 🔹 Use Volume

```bash
docker run -d -v myvolume:/data nginx
```

👉 Mounts volume inside container
👉 `/data` = container path
👉 Data **persists even if container is deleted** ✅

✅ **Example:**

```bash
docker run -d --name app -v ecommerce-data:/usr/share/nginx/html nginx
```

---

# 🔄 Additional Volume Commands (DevOps Must-Know)

---

## 🔍 List Volumes

```bash
docker volume ls
```

👉 Shows all volumes

---

## 🔎 Inspect Volume

```bash
docker volume inspect myvolume
```

👉 Shows storage location and details

---

## ❌ Remove Volume

```bash
docker volume rm myvolume
```

👉 Deletes volume (only if not in use)

---

## 🧹 Remove Unused Volumes

```bash
docker volume prune
```

👉 Cleans up unused volumes

---

# 🧪 Hands-On Lab (Important)

---

## 🎯 Step 1: Create Volume

```bash
docker volume create mydata
```

---

## 🎯 Step 2: Run Container with Volume

```bash
docker run -d --name web1 -v mydata:/usr/share/nginx/html nginx
```

---

## 🎯 Step 3: Add Data

```bash
docker exec -it web1 /bin/bash
echo "Hello DevOps" > /usr/share/nginx/html/index.html
exit
```

---

## 🎯 Step 4: Remove Container

```bash
docker rm -f web1
```

---

## 🎯 Step 5: Reuse Same Volume

```bash
docker run -d --name web2 -v mydata:/usr/share/nginx/html nginx
```

👉 Open browser → `http://localhost:8080` (if port mapped)
👉 Your data is still there ✅

---

# 🧠 DevOps Tips

👉 Use volumes for **databases (MySQL, MongoDB)**
👉 Never store important data inside container ❌
👉 Volumes are **independent of container lifecycle**
👉 Use bind mounts (`-v /host:/container`) for local dev

---

# ⚡ One-Line Summary

👉 **Docker Volume = Persistent storage independent of containers**

---


