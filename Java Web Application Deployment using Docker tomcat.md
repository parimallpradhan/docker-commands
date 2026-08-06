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
<img width="1751" height="72" alt="image" src="https://github.com/user-attachments/assets/3a0d4f8d-0059-48b5-b371-9a53f7be05ed" />

<img width="1748" height="132" alt="image" src="https://github.com/user-attachments/assets/c38d399d-a09e-499b-823a-653af03c7184" />

<img width="1692" height="145" alt="image" src="https://github.com/user-attachments/assets/d2d5a25a-9a4e-451e-81fe-d0b6d9aae0af" />


Verify:

```bash
docker --version
```
<img width="1762" height="55" alt="image" src="https://github.com/user-attachments/assets/80d8cd22-e67e-4bd4-94c6-918239e30b39" />

---

## 🌐 Step 2: Install Git

```bash
sudo apt install git -y
```

```bash
git --version
```
<img width="1607" height="145" alt="image" src="https://github.com/user-attachments/assets/6c783d87-db58-467d-a113-6f7c24b41530" />

---

## ☕ Step 3: Install Java & Maven

```bash
sudo apt update 
sudo apt install fontconfig openjdk-21-jre
java -version
sudo apt install maven -y
```

<img width="1682" height="120" alt="image" src="https://github.com/user-attachments/assets/1bc4f501-3ce3-4629-b80e-d6ee7d0e466e" />

```bash
java -version
mvn -version
```
<img width="1672" height="265" alt="image" src="https://github.com/user-attachments/assets/3b514e50-0641-42a3-9b5f-1d396781e969" />

---

## 📥 Step 4: Clone Repository

```bash
git clone https://github.com/parimallpradhan/ecommerce-app.git
cd ecommerce-app
```
<img width="1771" height="335" alt="image" src="https://github.com/user-attachments/assets/c958755c-5c8d-411a-9685-74fba8a99b21" />

---

## 📦 Step 5: Build Application

```bash
mvn clean package
```
<img width="1793" height="183" alt="image" src="https://github.com/user-attachments/assets/02a20680-2eaa-4008-94e7-2b817e250478" />

Output:

```text
target/ecommerce-app.war
```
<img width="1705" height="72" alt="image" src="https://github.com/user-attachments/assets/4d24b8a3-1218-4e5e-adae-f9eb0a68e38e" />

---

## 🐳 Step 6: Write Dockerfile

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
<img width="1572" height="387" alt="image" src="https://github.com/user-attachments/assets/a00aa4d6-459e-45e2-9a4b-39021efdf234" />


<img width="1866" height="90" alt="image" src="https://github.com/user-attachments/assets/ca69a37d-5830-45af-b8b8-fe12c0f0685c" />

---
## 🐳 Step 7: Build & Run Tomcat Container

```bash
# Build image
docker build -t ecommerce-app:v1 .
```
<img width="1627" height="298" alt="image" src="https://github.com/user-attachments/assets/36737f64-c429-4a8d-8fb3-4a89d2090b18" />

```bash
# Run container

docker run -d -p 8080:8080 --name ecommerce-app ecommerce-app:v1
```

```bash
docker ps
```
<img width="1707" height="135" alt="image" src="https://github.com/user-attachments/assets/0feeea8d-601d-445b-8d7d-753237c2a43f" />

---

## 🌍 Step 8: Access Application

```
http://<EC2-PUBLIC-IP>:8080/ecommerce-app
```

Example:

```
http://13.235.91.137:8080/ecommerce-app
```
<img width="1508" height="707" alt="image" src="https://github.com/user-attachments/assets/8192bd79-2727-4d58-bd89-e09ffa5f7e04" />

---


## ☁️ Step 9 :Now Tag image and Push to Docker Hub 
```bash
docker tag ecommerce-app:v1  parimal1984/ecommerce-app:v1
```
<img width="1517" height="200" alt="image" src="https://github.com/user-attachments/assets/5ecc49ff-7eaa-41db-82c0-4d63a1651273" />


```bash
docker login
docker push parimal1984/ecommerce-app:v1
```
<img width="1493" height="292" alt="image" src="https://github.com/user-attachments/assets/efb67a0f-abc9-4cd3-9a82-969b0018d010" />


<img width="1288" height="850" alt="image" src="https://github.com/user-attachments/assets/beaa5655-2bbd-4b7d-87eb-8b4da2e3214a" />


<img width="666" height="763" alt="image" src="https://github.com/user-attachments/assets/b7aed25a-6894-46e3-94c3-bb2bfb905627" />


```bash
docker push parimal1984/ecommerce-app:v1
```
<img width="1652" height="208" alt="image" src="https://github.com/user-attachments/assets/c3c20edd-8705-4f9e-8303-4ebe7a9fdc3f" />

<img width="1585" height="212" alt="image" src="https://github.com/user-attachments/assets/35f07ce2-52b6-4011-9bf6-5d2df681357a" />


---

---
skip below
---
## 📤 Step 8: Deploy WAR

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
