
[DockerQuestion](https://docs.google.com/document/d/1tLWIowoJGmsxamSHmYN1048t0QOK9i3jSBzUiHiZ9qA/edit?tab=t.0#heading=h.jtamaynsh313
)

# **🐳 Top 20 Scenario-Based Docker Interview Questions**

---

Docker One Shot Video : [https://yt.openinapp.co/7wgvn](https://yt.openinapp.co/7wgvn)

### **1️⃣ App works locally but fails in Docker. What do you check first?**

✅ Check:

* environment variables  
* exposed ports  
* Dockerfile CMD/ENTRYPOINT  
* application logs (`docker logs`)  
* file paths (Linux vs Windows)

---

### **2️⃣ Container exits immediately after starting. Why?**

✅ Main process finished execution.

Fix:

* ensure foreground process runs  
* check CMD / ENTRYPOINT  
* use `docker logs` to confirm error

---

### **3️⃣ App restarts but data is lost. Why?**

✅ Containers are ephemeral.

Fix:

* use Docker volumes or bind mounts.


---

### **4️⃣ Two containers cannot communicate. What’s the issue?**

✅ They are not on the same Docker network.

Fix:

* run via docker-compose  
* use service names, not IPs.

---

### **5️⃣ Why does `localhost` not work between containers?**

✅ `localhost` refers to the container itself.

Use:

`jdbc:mysql://mysql:3306`

---

### **6️⃣ Container works with `docker run` but fails in docker-compose. Why?**

Possible reasons:

* different env variables  
* different ports  
* volume path mismatch  
* missing depends\_on

---

### **7️⃣ How do you debug a running container?**

`docker exec -it container sh`

Then check logs, files, env vars.

---

### 

### **8️⃣ Docker image size is very large. How do you reduce it?**

✅ Use:

* slim images  
* multi-stage builds  
* `.dockerignore`  
* JRE instead of JDK

---

### **9️⃣ App connects to DB locally but fails in Docker. Why?**

Likely causes:

* using `localhost`  
* wrong DB hostname  
* DB not ready yet

---

### **🔟 How do you wait for DB before app starts?**

Options:

* healthcheck  
* retry logic  
* wait-for-it.sh  
* docker-compose condition

---

### **1️⃣1️⃣ Docker image runs old code even after rebuild. Why?**

✅ Docker layer caching.

Fix:

`docker build --no-cache`

---

### **1️⃣2️⃣ Environment variables not applied. Why?**

Reasons:

* variables defined in wrong service  
* container not rebuilt  
* OS env overriding YAML defaults

---

### **1️⃣3️⃣ How do you view container logs?**

`docker logs container-name`

Live:

`docker logs -f container-name`

---

### **1️⃣4️⃣ Container uses high memory unexpectedly. Why?**

Because JVM doesn’t know container limits.

Fix:

* container-aware JVM  
* memory flags  
* Java 17 handles this better.

---

### **1️⃣5️⃣ How do containers get IP addresses?**

Docker assigns IP automatically via bridge network.

DNS resolves service names to IP.

---

### 

### 

### **1️⃣6️⃣ How do you persist MySQL data in Docker?**

`volumes:`  
  `- mysql-data:/var/lib/mysql`

---

### **1️⃣7️⃣ How do you expose container to external world?**

`docker run -p 9090:8080 app`

Left \= host  
 Right \= container

---

### **1️⃣8️⃣ Why is container slower on Mac/Windows?**

Because Docker runs inside a VM.

Linux runs natively → faster.

---

### **1️⃣9️⃣ How do you stop all running containers?**

`docker stop $(docker ps -q)`

---

### **2️⃣0️⃣ When should you use Docker Compose?**

Use Compose when:

* multiple containers  
* networking required  
* volumes needed  
* environment-based config

