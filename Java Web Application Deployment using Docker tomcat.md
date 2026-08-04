# 🚀 Java Web Application Deployment using Docker & Tomcat on AWS EC2
---

````markdown


This project demonstrates an end-to-end deployment of a Java web application using:

- Git (Source Control)
- Maven (Build Tool)
- Docker (Containerization)
- Apache Tomcat (Application Server)
- AWS EC2 (Cloud Hosting)

---

## 📌 Architecture Overview

```text
GitHub Repository
      ↓
   Git Clone
      ↓
Maven Build (WAR)
      ↓
Docker Container (Tomcat)
      ↓
Deploy WAR → /webapps
      ↓
Application Live on EC2
````

---

## 🧱 Prerequisites

* AWS EC2 Instance (Ubuntu)
* Open Ports:

  * `22` (SSH)
  * `8080` (Application Access)

---

## 🐳 Step 1: Install Docker

```bash
sudo apt update
sudo apt install docker.io -y

sudo systemctl start docker
sudo systemctl enable docker

sudo usermod -aG docker ubuntu
newgrp docker
```

Verify:

```bash
docker --version
```

---

## 🌐 Step 2: Install Git

```bash
sudo apt install git -y
```

```bash
git --version
```

---

## ☕ Step 3: Install Java & Maven

```bash
sudo apt install openjdk-17-jdk -y
sudo apt install maven -y
```

```bash
java -version
mvn -version
```

---

## 📥 Step 4: Clone Repository

```bash
git clone https://github.com/<your-username>/ecommerce-app.git
cd ecommerce-app
```

---

## 📦 Step 5: Build Application

```bash
mvn clean package
```

Output:

```text
target/ecommerce-app.war
```

---

## 🐳 Step 6: Run Tomcat Container

```bash
docker run -d -p 8080:8080 --name tomcat1 tomcat
```

```bash
docker ps
```

---

## 📤 Step 7: Deploy WAR

```bash
docker cp target/ecommerce-app.war tomcat1:/usr/local/tomcat/webapps/
```

---

## 🔄 Step 8: Restart Container

```bash
docker restart tomcat1
```

---

## 🔍 Step 9: Verify Deployment

```bash
docker logs tomcat1
```

Expected log:

```text
Deploying web application archive
```

---

## 🌍 Step 10: Access Application

```
http://<EC2-PUBLIC-IP>:8080/ecommerce-app
```

Example:

```
http://13.235.91.137:8080/ecommerce-app
```

---

## 🔹 Optional: ROOT Deployment

```bash
docker cp target/ecommerce-app.war tomcat1:/usr/local/tomcat/webapps/ROOT.war
docker restart tomcat1
```

```
http://<EC2-IP>:8080/
```

---

## ⚠️ Troubleshooting

### 🔴 404 Error

* Check URL `/ecommerce-app`
* Restart container

### 🔴 WAR not deployed

```bash
docker logs tomcat1
```

### 🔴 Build issues

```bash
mvn clean package
```

---

## 💡 Best Practice (Volume Mount)

```bash
docker run -d -p 8080:8080 \
-v $(pwd)/target/ecommerce-app.war:/usr/local/tomcat/webapps/ecommerce-app.war \
--name tomcat1 tomcat
```

---

## 📷 Screenshot

![App Screenshot](https://github.com/user-attachments/assets/40c6a03d-e257-4e27-994c-04d52b62bed1)

---

## 👨‍💻 Author

**Parimal Pradhan**
[https://github.com/parimallpradhan](https://github.com/parimallpradhan)

```

---

# 🔥 Why This Works

- ✅ Code blocks are **only where needed**
- ✅ No nested backticks (main issue earlier)
- ✅ Architecture diagram uses `text` block (clean display)
- ✅ Proper spacing for GitHub renderer

---

# 🚀 If You Want It Even Better

I can upgrade your README with:
- 📊 :contentReference[oaicite:0]{index=0}
- 🐳 :contentReference[oaicite:1]{index=1}
- 🔁 :contentReference[oaicite:2]{index=2}
- 🏷️ :contentReference[oaicite:3]{index=3}

Just say 👍
```
