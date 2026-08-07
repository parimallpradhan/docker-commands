Perfect 👌 — this is now a **complete classroom-ready version** with:

✅ Simple explanation
✅ Real-life analogy
✅ Hands-on commands


---

# 🐳 Dockerfile Instructions (Easy + Hands-On + Real-Time Tasks)

---

## 1️⃣ FROM → Base Image (Foundation)

### 👉 Think like

🏠 Foundation of a house

### 📘 Purpose

Defines base OS/image

### ✅ Example

```dockerfile
FROM ubuntu:24.04
```

### 🧪 Hands-on

```bash
docker pull ubuntu:24.04
docker run -it ubuntu:24.04 bash
```

### 🎯 Real-time Task

👉 * Run Ubuntu container
    * Check OS version:

```bash
cat /etc/os-release
```

---

## 2️⃣ RUN → Install Software

### 👉 Think like

📦 Installing apps on your laptop

### 📘 Purpose

Runs commands during build

### ✅ Example

```dockerfile
RUN apt-get update && apt-get install -y curl
```

### 🧪 Hands-on

```bash
docker build -t myimage:v1 .
docker run myimage:v1 curl --version
```

### 🎯 Real-time Task

👉 Students install:

* `vim` or `git` inside container

```dockerfile
RUN apt-get install -y vim
```

---

## 3️⃣ COPY → Copy Files

### 👉 Think like

📁 Copy file from your system → container

### 📘 Purpose

Copy files into container

### ✅ Example

```dockerfile
COPY test.txt /app/
```

### 🧪 Hands-on

```bash
echo "Hello Docker" > test.txt
docker build -t copy-demo .
docker run copy-demo cat /app/test.txt
```

### 🎯 Real-time Task

👉 Students:

* Create their own file
* Display inside container

---

## 4️⃣ ADD → Smart Copy

### 👉 Think like

📦 Copy + unzip automatically

### 📘 Purpose

Copy + extract files

### ✅ Example

```dockerfile
ADD files.tar.gz /app/
```

### 🧪 Hands-on

Create tar file:

```bash
tar -czf files.tar.gz test.txt
```

### 🎯 Real-time Task

👉 Students:

* Add `.tar.gz` file
* Verify extraction inside container

---

## 5️⃣ WORKDIR → Change Directory

### 👉 Think like

📂 cd into folder

### 📘 Purpose

Set working directory

### ✅ Example

```dockerfile
WORKDIR /app
```

### 🧪 Hands-on

```dockerfile
WORKDIR /app
RUN pwd
```

### 🎯 Real-time Task

👉 Students:

* Create file using WORKDIR

```dockerfile
RUN touch demo.txt
```

---

## 6️⃣ EXPOSE → Port Info


### 👉 Think like

🌐 App runs on this port

### 📘 Purpose

Documents port

### ✅ Example

```dockerfile
EXPOSE 8080
```

### 🧪 Hands-on

```bash
docker run -p 8080:8080 image-name
```

### 🎯 Real-time Task

👉 Students:

* Run nginx:

```bash
docker run -d -p 8080:80 nginx
```

* Open browser → localhost:8080

---

## 7️⃣ ENV → Environment Variables

### 👉 Think like

⚙️ App settings

### 📘 Purpose

Store config values

### ✅ Example

```dockerfile
ENV MY_NAME=Student
```

### 🧪 Hands-on

```bash
docker run image-name env
```

### 🎯 Real-time Task

👉 Students:

* Print variable:

```dockerfile
CMD ["sh","-c","echo $MY_NAME"]
```

---

## 8️⃣ LABEL → Metadata

### 👉 Think like

🏷️ Tag info

### 📘 Purpose

Add metadata

### ✅ Example

```dockerfile
LABEL version="1.0"
LABEL trainer="parimal"
```

### 🧪 Hands-on

```bash
docker inspect image-name
```

### 🎯 Real-time Task

👉 Students:

* Add their name as label
* Verify using inspect

---

## 9️⃣ CMD → Default Command

### 👉 Think like

▶️ Default program

### 📘 Purpose

Runs when container starts

### ✅ Example

```dockerfile
CMD ["echo","Hello Students"]
```

### 🧪 Hands-on

```bash
docker run image-name
```

### 🎯 Real-time Task

👉 Students:

* Change output message
* Override CMD:

```bash
docker run image-name echo "Hi"
```

---

## 🔟 ENTRYPOINT → Main App

### 👉 Think like

🚀 Main application

### 📘 Purpose

Fixed command

### ✅ Example

```dockerfile
ENTRYPOINT ["echo"]
CMD ["Hello"]
```

### 🧪 Hands-on

```bash
docker run image-name
```

### 🎯 Real-time Task

👉 Students:

* Try overriding:

```bash
docker run image-name Hi
```

---

# ⚔️ CMD vs ENTRYPOINT

| CMD          | ENTRYPOINT |
| ------------ | ---------- |
| Can override | Fixed      |
| Default      | Main app   |

---

# 🧪 FINAL HANDS-ON PROJECT (Mini Lab)

### 📄 Dockerfile

```dockerfile
FROM alpine:3.20

WORKDIR /app

COPY test.txt /app/

ENV MY_NAME=Student

LABEL version="1.0"

CMD ["sh","-c","echo Hello $MY_NAME && cat /app/test.txt"]
```

---

### ▶️ Steps

```bash
# Step 1
echo "Welcome to Docker Lab" > test.txt

# Step 2
docker build -t student-demo:v1 .

# Step 3
docker run student-demo:v1
```

---






