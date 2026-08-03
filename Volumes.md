# 💾 6. Volumes (Data Persistence)

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


