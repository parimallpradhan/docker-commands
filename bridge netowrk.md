# 🚀 1. **Bridge network = Private network where containers can talk**

---

# 🔹 2. Default Bridge Network (docker0)


### 💡 Explanation:

* Docker automatically creates this network
* Name = `bridge` (internally docker0)
* Every container goes here by default

---

### 🧠 Key Point:

👉 Containers **CAN communicate using IP**
👉 Containers **CANNOT communicate using name**

---

### 🧪 Hands-on Demo:

```bash
# Run 2 containers (default network)
docker run -dit --name c1 alpine sh
docker run -dit --name c2 alpine sh
```

---

### 🔍 Check network:

```bash
docker network inspect bridge
```

👉 Show students:

* IP addresses assigned

---

### 📡 Test Communication (IMPORTANT):

```bash
docker exec -it c1 sh

apt update
apt install -y iputils-ping
```

Inside container:

```bash
ping c2
```

❌ **Fails** (name not resolved)

---

👉 Now try with IP:

```bash
ping <c2-ip>
```

✅ Works

---

### ❌ Problem with Default Bridge:

* No DNS (name resolution ❌)
* Not scalable
* Hard to manage

---

---

# 🔹 3. Named Bridge Network (User-Defined)

![Image](https://images.openai.com/static-rsc-4/J79ILc93OQvxFuBVsy0Wvn1fRuMoMGLn1Sk6zdYA0BxCnLajOOrX_3iMrVBJuID5qzeQXJjY6JKJ4icsMXUB7UGbbGxtQnbsLWwjR4TBJZpBV2nPkn2BdPm-pVddaeFS9EHRHMFfUOSNfYwdd8B1p7P3AQouIRYAMMI3KsCHHXkiuaTn5qS7aJpKLAwP8OXZ?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/P4861Aud649hfumLfHAFrGe4iwwJUgbXvG0E7NiY9VAvvtc_xyi_9uOYNdFZK6OBZ5peaI6Za9fvObQdMs41nOwi-oG2mKoM3ni9aGePr5aOLddFcX-_UvMnRi9OhXCZFIcqC94U0Y9qg4NdNwGTBp3sfF_ZuxjYg7eTXG_-oN-xtHYi8sD9x-4QQAnNctfT?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/G71uyHxUryTPQCOVxcxiHHJ7HAs9U4wsU7pb_inPNiiUmCEX_CeXftLWEPJMkyDvG72j3UEcFexMHiwuNvecBxDKSAHFk2CN2ZtC5c2P0SGfRFTbukNKsZ17NOEFVGDeymOE8Xx9NPhtO9Qgh1DLNB4sDXhHByLfn49SwcqxC-aCND-aaFwZw-zCyGgB0CUy?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/eNmNNdDjEikrA5KrAU4R4n6P-C2RG59d5HjP1fALt6AQr2FMtW3o0ljjHkJRAeCdmoHsUXEFmrFEJSWiS0m4xzPGISAD9eeNss6WkBQynCMi0m-4DgoZTv-Q58SXZiCQrd7BaYUBiOW7qxNJqFQZqAIhKg3CPSIrCgqud76qGSyGiq5Z9fTNl8Ctzn7OyuH6?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/zY72UT6yEQFAY4bzpPMOyMTewCrOFGNjXmFQJxTeaQHVU1Izp2t5yV-QTXIiZ35aBlqW8LhHX6j2sSlxYkI3kDDE_d2g3VjW-WMVfTEEnPPwir7NphA0bq1hLwmPfjdX7OG-RROvNbGpNpeo4DoxkbMm0rnXwdIp6sDIW8UkIApvbAdfkqYRyAqyMAGZ7ISg?purpose=fullsize)

### 💡 Simple Explanation:

* Network created by YOU
* Has built-in DNS
* Containers talk using **names**

---

### 🎯 Key Advantage:

👉 `container-name = hostname`

---

### 🧪 Hands-on Demo:

```bash
# Create custom network
docker network create my-net
```

```bash
# Run containers in that network
docker run -dit --name c1 --network my-net alpine sh
docker run -dit --name c2 --network my-net alpine sh
```

---

### 📡 Test Communication:

```bash
docker exec -it c1 sh
```

Inside container:

```bash
ping c2
```

✅ SUCCESS 🎉

---

### 🔥 Highlight This Line:

> In named bridge → Docker provides **automatic DNS**

---

---

# ⚡ 4. Side-by-Side Difference (Very Important)

| Feature               | Default Bridge      | Named Bridge |
| --------------------- | ------------------- | ------------ |
| Created by            | Docker              | User         |
| DNS (name resolution) | ❌ No                | ✅ Yes        |
| Communication         | IP only             | Name + IP    |
| Best for              | Testing             | Real apps    |
| Example               | Quick container run | App + DB     |

---

---

# 🎯 5. Real-Time Example (Make it relatable)

### ❌ Default Bridge (Problem)

```bash
jdbc:mysql://172.17.0.2:3306/db
```

👉 If container restarts → IP changes ❌

---

### ✅ Named Bridge (Solution)

```bash
jdbc:mysql://mysql:3306/db
```

👉 Always works ✅

---

---

# 💣 6. Mistake to Show Students

```bash
docker run -d --name app nginx
docker run -d --name db mysql
```

👉 Ask:

> “Why app cannot connect DB?”

---

Then fix:

```bash
docker network create app-net

docker network connect app-net app
docker network connect app-net db
```


---



---

---

# 🏁 Final One-Line Summary

👉 **Default bridge = IP-based communication**
👉 **Named bridge = Name-based communication (Best Practice)**

---

