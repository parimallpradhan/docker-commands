# 🚀 🔹 Overlay Network Demo (2 EC2 Instances)

---

## 🧠 1. One-Line Concept

> **Overlay network = Connect containers across multiple machines**

---

## 🖼️ Architecture (Explain First)


👉 Explain:

* EC2-1 → Manager
* EC2-2 → Worker
* Overlay network connects both
* Containers talk using **name (DNS)**

---

# ⚙️ 2. Prerequisites

👉 Both EC2 instances:

* Amazon Linux / Ubuntu ✅
* Docker installed ✅
* Security Group: Allow all traffic between instances

  * TCP: 2377 (Swarm)
  * TCP/UDP: 7946 (communication)
  * UDP: 4789 (overlay network)

---

# 🧪 3. Step-by-Step Demo

---

## 🔹 Step 1: Initialize Swarm (EC2-1)

```bash
docker swarm init
```

👉 Output will show:

```bash
docker swarm join --token <TOKEN> <MANAGER-IP>:2377
```

---

## 🔹 Step 2: Join Worker (EC2-2)

Copy command and run on EC2-2:

```bash
docker swarm join --token <TOKEN> <MANAGER-IP>:2377
```

---

## 🔹 Step 3: Verify Nodes (Run on Manager)

```bash
docker node ls
```

✅ You should see:

* 1 Manager
* 1 Worker

---

## 🔹 Step 4: Create Overlay Network

```bash
docker network create -d overlay my-overlay
```

---

## 🔹 Step 5: Run Containers on Different Nodes

👉 Run nginx on manager:

```bash
docker service create \
  --name web \
  --network my-overlay \
  --replicas 1 \
  nginx
```

---

👉 Run alpine container (interactive test):

```bash
docker service create \
  --name test \
  --network my-overlay \
  alpine sleep 10000
```

---

## 🔹 Step 6: Check where containers are running

```bash
docker service ps web
docker service ps test
```

👉 Some may run on EC2-1, some on EC2-2

---

## 🔹 Step 7: Test Communication (IMPORTANT)

Get container ID:

```bash
docker ps
```

Enter container:

```bash
docker exec -it <container-id> sh
```

Now test:

```bash
ping web
```

✅ SUCCESS 🎉

👉 Even if `web` is on **another EC2**

---

# 💥 4. Key Teaching Moment

Ask students:

👉 “How is this working across servers?”

Answer:

> Overlay network creates a **virtual network across machines**

---

# ⚡ 5. Real-Time Use Case

### 🛒 E-commerce Microservices

* EC2-1 → Product service
* EC2-2 → Cart service
* EC2-3 → Payment service

👉 All communicate using:

```bash
http://product-service
http://cart-service
```

---

# ⚠️ 6. Common Mistakes (Must Show)

---

### ❌ Swarm not initialized

```bash
docker network create -d overlay my-net
```

👉 ERROR

✔ Fix → Run `docker swarm init`

---

### ❌ Ports not open in Security Group

👉 Overlay will NOT work

---

### ❌ Using docker run

```bash
docker run --network my-overlay nginx
```

👉 ❌ Not supported

✔ Use:

```bash
docker service create
```

---

# 🧠 7. Difference Recap

| Network | Scope            |
| ------- | ---------------- |
| Bridge  | Single machine   |
| Host    | Single machine   |
| None    | No network       |
| Overlay | 🔥 Multi-machine |

---

# 🎯 8. Teaching Flow (Perfect Classroom Demo)

1. Show 2 EC2 instances
2. Init swarm
3. Join worker
4. Create overlay
5. Run services
6. Show containers on different machines
7. Ping using name
8. Ask: “Same network or different?”

---

# 🏁 Final One-Line Summary

👉 **Overlay network = Connect containers across multiple servers like they are on same network**

---

## 🚀 Want Next Level?

I can help you with:

✅ Full microservices deployment across EC2
✅ Spring Boot services on overlay network
✅ Load balancing using Docker Swarm
✅ Kubernetes comparison (overlay vs CNI)

Just tell me 👍
