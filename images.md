# 🐳 Docker Image Commands (Number-wise with Examples)

---

## 📦 1. Pull Image

```bash
docker pull nginx
```

👉 Downloads an image from Docker Hub

✅ **Example:**
Pull nginx image to run a web server

---

## 📦 2. List Images

```bash
docker images
```

👉 Shows all images on your system

✅ **Example Output:**

```
REPOSITORY   TAG     IMAGE ID
nginx        latest  abc123
```

---

## 📦 3. Remove Image

```bash
docker rmi nginx
```

👉 Deletes an image

✅ **Example:**
Remove unused nginx image to free space

---

## 🔍 4. Search Images

```bash
docker search nginx
```

👉 Searches Docker Hub for images

✅ **Example:**
Find official nginx image and alternatives

---

## 📥 5. Pull Specific Version

```bash
docker pull nginx:1.25
```

👉 Pulls a specific version

✅ **Example:**
Use stable version in production instead of latest

---

## 🏷️ 6. Tag Image

```bash
docker tag nginx mynginx:v1
```

👉 Creates a new tag

✅ **Example:**
Prepare image before pushing to Docker Hub

---

## 📤 7. Push Image

```bash
docker push mynginx:v1
```

👉 Uploads image to registry

✅ **Example:**
Push image to Docker Hub for CI/CD pipeline

---

## 🔑 8. Login to Docker Hub

```bash
docker login
```

👉 Authenticate before push

✅ **Example:**
Login using Docker Hub credentials

---

## 📜 9. Image History

```bash
docker history nginx
```

👉 Shows image layers

✅ **Example:**
Understand how image was built step-by-step

---

## 🔎 10. Inspect Image

```bash
docker inspect nginx
```

👉 Detailed JSON info

✅ **Example:**
Check environment variables, config, layers

---

## 📦 11. Save Image (Backup)

```bash
docker save -o nginx.tar nginx
```

👉 Save image as file

✅ **Example:**
Transfer image to another server offline

---

## 📥 12. Load Image

```bash
docker load -i nginx.tar
```

👉 Load saved image

✅ **Example:**
Restore image from backup

---

## 🧹 13. Remove Dangling Images

```bash
docker image prune
```

👉 Cleans unused images

✅ **Example:**
Free disk space in CI/CD server

---

## 🗑️ 14. Remove All Images

```bash
docker rmi $(docker images -q)
```

👉 Deletes all images ⚠️

✅ **Example:**
Clean system before fresh setup

---

## 🔄 15. Pull All Tags

```bash
docker pull --all-tags nginx
```

👉 Download all versions

✅ **Example:**
Test multiple versions locally

---

## 🧱 16. Build Image Without Cache

```bash
docker build --no-cache -t myapp:v2 .
```

👉 Forces fresh build

✅ **Example:**
Avoid cached dependencies in CI pipeline

---

## 📊 17. Show Image Size

```bash
docker images
```

👉 Displays size

✅ **Example:**
Identify large images to optimize

---

## 🧪 18. Run Image (Auto Remove Container)

```bash
docker run --rm nginx
```

👉 Temporary container

✅ **Example:**
Run quick test without saving container

---


