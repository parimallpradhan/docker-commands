# 🔍 Docker Debugging & Logs Commands

---

## 📜 1. View Logs

```bash id="7kq9xv"
docker logs <container_id>
```

👉 Shows application logs from the container

✅ **Example:**

```bash id="u5k2nd"
docker logs abc123
```

👉 Displays nginx/server logs

---

### 🔥 Useful Variations

```bash id="9nq3hy"
docker logs -f abc123
```

👉 **Follow logs (live streaming)**

```bash id="m2v8qp"
docker logs --tail 50 abc123
```

👉 Show last 50 lines

---

## 💻 2. Exec into Container

```bash id="c8z1re"
docker exec -it <container_id> /bin/bash
```

👉 Access container terminal

✅ **Example:**

```bash id="k6x4mz"
docker exec -it abc123 /bin/bash
```

👉 Now you can run:

```bash id="q2f7vb"
ls
ps -ef
cat /var/log/nginx/access.log
```

---

### ⚡ If bash not available

```bash id="x9w3pl"
docker exec -it abc123 /bin/sh
```

---

## 🔎 3. Inspect Container

```bash id="4p8tjy"
docker inspect <container_id>
```

👉 Detailed JSON info about container

---

### ✅ Example:

```bash id="n7d2ac"
docker inspect abc123
```

👉 You can find:

* IP Address 🌐
* Mounted volumes 💾
* Environment variables ⚙️
* Network details 🔗

---

### 🔥 Extract Specific Info

```bash id="z1y9hd"
docker inspect -f '{{.NetworkSettings.IPAddress}}' abc123
```

👉 Get container IP directly

---

# 🧪 Hands-On Debugging Lab

---

## 🎯 Step 1: Run Container

```bash id="x7k3pt"
docker run -d -p 8080:80 --name mynginx nginx
```

---

## 🎯 Step 2: Check Logs

```bash id="y4h8zw"
docker logs mynginx
```

---

## 🎯 Step 3: Access Container

```bash id="r9q6cl"
docker exec -it mynginx /bin/bash
```

---

## 🎯 Step 4: Inspect Container

```bash id="p5n2mx"
docker inspect mynginx
```

---

# 🧠 DevOps Debugging Tips

👉 If app not working:

1. Check logs first 🔥
2. Exec into container 🔍
3. Inspect config ⚙️

---

# ⚡ One-Line Summary

👉 **Logs + Exec + Inspect = Complete Docker debugging toolkit**

---

