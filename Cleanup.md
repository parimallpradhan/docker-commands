# 🧹 7. Cleanup 

---

## 🔹 Remove All Stopped Containers

```bash id="c1m2q8"
docker container prune
```

👉 Deletes all **stopped containers**
👉 Helps free up space

⚠️ Prompts for confirmation (`y/n`)

✅ **Example Use Case:**
After testing multiple containers, clean unused ones

---

## 🔹 Remove Unused Images

```bash id="m7d9ks"
docker image prune
```

👉 Removes **dangling images** (unused/intermediate)
👉 Frees disk space

✅ **Optional (More Cleanup):**

```bash id="7pz2xf"
docker image prune -a
```

👉 Removes **all unused images**, not just dangling

---

## 🔹 Remove Everything (Careful ⚠️)

```bash id="0k4x8n"
docker system prune -a
```

👉 Deletes:

* Stopped containers
* Unused images
* Unused networks
* Build cache

⚠️ **Very powerful command — use carefully**

---

# 🔄 Additional Cleanup Commands (Good to Know)

---

## 🧹 Remove Unused Volumes

```bash id="9u3z2r"
docker volume prune
```

👉 Deletes unused volumes

---

## 🌐 Remove Unused Networks

```bash id="g4q8t1"
docker network prune
```

👉 Cleans unused networks

---

## 📊 Check Disk Usage

```bash id="2h8sdf"
docker system df
```

👉 Shows space used by images, containers, volumes

---

# 🧪 Hands-On Lab (Recommended)

---

## 🎯 Step 1: Create Test Containers

```bash id="p9w3jd"
docker run -d nginx
docker run -d nginx
docker stop $(docker ps -aq)
```

---

## 🎯 Step 2: Cleanup Stopped Containers

```bash id="z8x4cb"
docker container prune
```

---

## 🎯 Step 3: Remove Unused Images

```bash id="u1m7qn"
docker image prune -a
```

---

## 🎯 Step 4: Full Cleanup

```bash id="5r2k8p"
docker system prune -a
```

---

# 🧠 DevOps Tips

👉 Run cleanup regularly in **CI/CD pipelines**
👉 Use `docker system df` before cleanup to analyze usage
👉 Avoid deleting volumes unless sure (data loss risk ⚠️)
👉 Automate cleanup using cron jobs (Linux servers)

---

# ⚡ One-Line Summary

👉 **Docker Cleanup = Free space + keep environment clean**

---

