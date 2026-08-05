# 🌐 5. Networking

## What is Docker Networking?

**Docker Networking** is the feature that allows Docker containers to communicate with:

* Other containers
* The Docker host (your EC2 instance or local machine)
* External networks (Internet)
* Other physical or virtual servers

Think of Docker networking like a company's office network.

* Each **container** is an employee.
* Each employee has a desk (IP address).
* The office network allows employees to talk to each other.
* Some employees can also communicate with customers outside the company (Internet).

Without networking, containers would be isolated and unable to communicate.

---

## Why Do We Need Docker Networking?

Imagine you have an E-commerce application.

```
+-----------------------+
|   Customer Browser    |
+----------+------------+
           |
           |
       Internet
           |
      Docker Host (EC2)
           |
   -------------------------
   |          |            |
Frontend   Backend      MySQL
Container  Container   Container
```

* Frontend needs Backend
* Backend needs Database
* Customers need Frontend

Docker networking makes all of these communications possible.

---

## Real-Time Example

Suppose your application has three containers.

```
Container 1 : Nginx
Container 2 : Spring Boot
Container 3 : MySQL
```

Communication flow:

```
User
   |
   v
Nginx Container
      |
      v
Spring Boot Container
      |
      v
MySQL Container
```

Without Docker networking, the Spring Boot container cannot connect to MySQL.

---

## How Docker Networking Works

When Docker starts, it creates a virtual network.

Every container connected to that network receives:

* An IP Address
* A Network Interface
* A Gateway

Example

```
Docker Host (EC2)

Docker Network
----------------------------

Container A
IP : 172.17.0.2

Container B
IP : 172.17.0.3

Container C
IP : 172.17.0.4
```

Containers communicate using these IP addresses or, more commonly, by **container name** on user-defined networks.

---

## Real-Time Banking Example

Suppose a banking application consists of:

```
Customer Portal
Account Service
Payment Service
Database
```

Running in Docker:

```
Customer Portal Container
          |
          |
Account Service Container
          |
          |
Payment Service Container
          |
          |
MySQL Container
```

All containers communicate over a Docker network.

---

## Types of Docker Networks

Docker provides several network drivers.

| Network Type | Description                                            | Real-Time Use Case                                  |
| ------------ | ------------------------------------------------------ | --------------------------------------------------- |
| **Bridge**   | Default network for containers on the same Docker host | Web App + Database on one EC2 instance              |
| **Host**     | Container shares the host's network                    | High-performance applications                       |
| **None**     | No networking                                          | Secure isolated container                           |
| **Overlay**  | Connects containers across multiple Docker hosts       | Docker Swarm or multi-host deployments              |
| **Macvlan**  | Gives each container its own MAC and LAN IP            | Legacy applications that need direct network access |

---

# 1. Bridge Network (Most Common)

When you install Docker, it automatically creates a default bridge network.

```
Docker Host (EC2)

       docker0 Bridge
     --------------------
      |       |       |
   App1     App2    MySQL
```

Example:

```bash
docker network ls

NETWORK ID     NAME      DRIVER
xxxx           bridge    bridge
```

Run containers:

```bash
docker run -d --name app nginx

docker run -d --name mysql mysql
```

They are connected to the bridge network.

---

## 2. Host Network

The container uses the host machine's network directly.

```
Normal

Container ---> Bridge ---> EC2

Host Mode

Container ---------> EC2 Network
```

Example:

```bash
docker run --network host nginx
```

Advantages:

* Faster
* No NAT
* Better performance

Disadvantage:

* No network isolation.

---

## 3. None Network

No networking at all.

```
Container

No Internet
No Other Containers
No Network
```

Example

```bash
docker run --network none alpine
```

Used for:

* Security testing
* Offline processing
* Sensitive workloads

---

## 4. Overlay Network

Used when containers are on different Docker hosts.

Example

```
EC2-1
App Container
      \
       \
     Overlay Network
       /
      /
EC2-2
Database Container
```

Mostly used with **Docker Swarm**.

---

## 5. Macvlan Network

The container gets its own IP on the physical LAN.

```
Router
   |
Switch
 |      |
EC2    Container
       IP:192.168.1.50
```

Useful for applications that need to appear as separate devices on the network.

---

# Real-Time Example: Spring Boot + MySQL

Suppose you run:

```bash
docker run --name mysql mysql
```

and

```bash
docker run --name ecommerce-app ecommerce:v1
```

If they are connected to the same user-defined bridge network:

```
Docker Network

+----------------------+
| ecommerce-app        |
|      |               |
|      | mysql:3306    |
|      v               |
|     mysql            |
+----------------------+
```

Instead of using an IP address, the application can connect using:

```properties
spring.datasource.url=jdbc:mysql://mysql:3306/ecommerce
```

Here, `mysql` is the **container name**, which Docker resolves automatically on a user-defined bridge network.

---

# Docker Networking Commands

### List networks

```bash
docker network ls
```

### Inspect a network

```bash
docker network inspect bridge
```

### Create a network

```bash
docker network create my-network
```

### Run a container in a network

```bash
docker run -d --network my-network nginx
```

### Connect a running container to a network

```bash
docker network connect my-network container_name
```

### Disconnect a container

```bash
docker network disconnect my-network container_name
```

### Remove a network

```bash
docker network rm my-network
```

---

# Interview Questions

**1. What is Docker Networking?**
Docker Networking is the mechanism that enables containers to communicate with each other, the Docker host, and external networks.

**2. What is the default Docker network?**
`bridge`.

**3. Which network is used for multiple Docker hosts?**
`overlay`.

**4. Which network provides the best performance?**
`host`, because it bypasses Docker's network isolation layer.

**5. Which network completely isolates a container?**
`none`.

---

## Summary

| Network Type | Communication                    | Typical Use Case                         |
| ------------ | -------------------------------- | ---------------------------------------- |
| Bridge       | Containers on the same host      | Most applications (default)              |
| Host         | Container uses host network      | Performance-sensitive workloads          |
| None         | No communication                 | Secure or isolated jobs                  |
| Overlay      | Containers across multiple hosts | Docker Swarm / clustered deployments     |
| Macvlan      | Container gets a LAN IP          | Legacy or network appliance applications |



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




