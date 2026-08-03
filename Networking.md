# 🌐 5. Networking

---

## 🔹 List Networks

```bash
docker network ls
```

👉 Shows all available Docker networks
👉 Default networks: `bridge`, `host`, `none`

✅ **Example Output:**

* bridge
* host
* none
* mynetwork

---

## 🔹 Create Network

```bash
docker network create mynetwork
```

👉 Creates a custom network
👉 Containers inside can communicate using names (DNS)

✅ **Example:**

```bash
docker network create ecommerce-net
```

---

## 🔹 Run Container in Network

```bash
docker run -d --network=mynetwork nginx
```

👉 Starts container inside specific network
👉 Enables communication with other containers

✅ **Example:**

```bash
docker run -d --name web --network=ecommerce-net nginx
```

---

# 🔄 Additional Useful Networking Commands (DevOps Must-Know)

---

## 🔍 Inspect Network

```bash
docker network inspect mynetwork
```

👉 Shows detailed info (connected containers, IPs)

---

## 🔗 Connect Running Container to Network

```bash
docker network connect mynetwork <container_id>
```

👉 Attach existing container to network

---

## ❌ Disconnect Container from Network

```bash
docker network disconnect mynetwork <container_id>
```

---

## 🗑️ Remove Network

```bash
docker network rm mynetwork
```

👉 Deletes network (must not be in use)

---

# 🧪 Hands-On Lab (Important)

---

## 🎯 Step 1: Create Network

```bash
docker network create app-net
```

---

## 🎯 Step 2: Run Backend Container

```bash
docker run -d --name backend --network=app-net nginx
```

---

## 🎯 Step 3: Run Frontend Container

```bash
docker run -d --name frontend --network=app-net busybox sleep 3600
```

---

## 🎯 Step 4: Test Connectivity

```bash
docker exec -it frontend ping backend
```

👉 **Result:** Containers communicate using name (`backend`)
👉 No need for IP address ❌

---




