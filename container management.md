# 🐳 Docker Container Commands 

---

## 🚀 1. Run Container

```bash id="5tw2yl"
docker run -d -p 8080:80 nginx
```

👉 Creates & starts container in background
👉 Maps port **8080 → 80**

✅ **Example:**
Run nginx web server → open `http://localhost:8080`

---

## 📋 2. List Running Containers

```bash id="i8pl2k"
docker ps
```

👉 Shows active containers

✅ **Example Output:**

```id="s5pjwd"
CONTAINER ID   IMAGE   PORTS
abc123         nginx   0.0.0.0:8080->80
```

---

## 📋 3. List All Containers

```bash id="k9z9vr"
docker ps -a
```

👉 Shows running + stopped containers

✅ **Example:**
Check previously stopped containers

---

## ⛔ 4. Stop Container

```bash id="r7yz55"
docker stop <container_id>
```

✅ **Example:**

```bash id="f4j3kp"
docker stop abc123
```

👉 Stops running nginx container

---

## ▶️ 5. Start Container

```bash id="6qxpd3"
docker start <container_id>
```

✅ **Example:**

```bash id="1vgt0h"
docker start abc123
```

👉 Restarts stopped container

---

## 🗑️ 6. Remove Container

```bash id="r7f5jk"
docker rm <container_id>
```

✅ **Example:**

```bash id="2xdl7l"
docker rm abc123
```

👉 Deletes container permanently

---

# 🔍 Additional Important Container Commands

---

## 🧾 7. View Logs

```bash id="jgl5os"
docker logs <container_id>
```

👉 Shows application logs

✅ **Example:**

```bash id="q5mq4l"
docker logs abc123
```

---

## 💻 8. Exec into Container

```bash id="xq91h7"
docker exec -it <container_id> /bin/bash
```

👉 Access container terminal

✅ **Example:**

```bash id="1jyb2f"
docker exec -it abc123 /bin/bash
```

---

## 🔍 9. Inspect Container

```bash id="ik9nq9"
docker inspect <container_id>
```

👉 Detailed container info

✅ **Example:**
Check IP address, config, mounts

---

## 🔁 10. Restart Container

```bash id="r5v41z"
docker restart <container_id>
```

✅ **Example:**

```bash id="z8dxt3"
docker restart abc123
```

👉 Stops + starts container

---

## 🧹 11. Remove All Stopped Containers

```bash id="rz5htm"
docker container prune
```

👉 Cleans unused containers

✅ **Example:**
Free space in server

---

## ⚡ 12. Run Container with Name

```bash id="9p7d6o"
docker run -d -p 8081:80 --name mynginx nginx
```

✅ **Example:**
Access container using name instead of ID

---

## 🔄 13. Run Container in Interactive Mode

```bash id="3m9s2r"
docker run -it ubuntu /bin/bash
```

👉 Opens terminal

✅ **Example:**
Use Ubuntu container like a VM

---

## 🧪 14. Auto Remove Container

```bash id="r6zjv3"
docker run --rm nginx
```

👉 Deletes container after stop

✅ **Example:**
Temporary testing container

---

## 🌐 15. Port Mapping Example

```bash id="n1b0yx"
docker run -d -p 9090:80 nginx
```

✅ **Example:**
Access app → `http://localhost:9090`

---

# 🧠 Final Quick Tip

👉 Use **container name instead of ID** for easy management
👉 Example:

```bash id="g3o6xq"
docker stop mynginx
```

---
