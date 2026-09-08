

# Containerize a Spring Boot Application

## 1. Build the Spring Boot Application

Using Maven:

```bash
mvn clean package -DskipTests
```

This generates:
[]()
```text
target/app.jar
```

---

## 2. Create a Dockerfile

Create `Dockerfile` in the project root:


Mental model:

```text
FROM
 ↓
Java Runtime

WORKDIR
 ↓
/app

COPY
 ↓
JAR → /app/app.jar

EXPOSE
 ↓
Application listens on 8080

ENTRYPOINT
 ↓
java -jar app.jar
```

---

# 3. Build Docker Image

Run:

```bash
docker build -t springboot-app:1.0 .
```

Meaning:

```text
docker build
     ↓
Build an image

-t springboot-app:1.0
     ↓
Image name + tag

.
     ↓
Current directory = Build Context
```

Check the image:

```bash
docker images
```

---

# 4. Create and Run Container

```bash
docker run -d \
  --name springboot-container \
  -p 8080:8080 \
  springboot-app:1.0
```

Flow:

```text
Browser
   │
   │ localhost:8080
   ▼
Host :8080
   │
   │ -p 8080:8080
   ▼
Container :8080
   │
   ▼
Spring Boot
```

---

# 5. Check Container

```bash
docker ps
```

Check logs:

```bash
docker logs springboot-container
```

Follow logs:

```bash
docker logs -f springboot-container
```

---

# 6. Access the Application

Open:

```text
http://localhost:8080
```

The request flow is:

```text
Client
  ↓
localhost:8080
  ↓
Docker Port Mapping
  ↓
Container:8080
  ↓
Spring Boot Application
```

---

# Important Docker Commands

|**Command**|**Purpose**|
|---|---|
|`mvn clean package`|Build Spring Boot JAR|
|`docker build -t springboot-app:1.0 .`|Build Docker image|
|`docker images`|List images|
|`docker run -d -p 8080:8080 springboot-app:1.0`|Create + start container|
|`docker ps`|List running containers|
|`docker logs <container>`|View logs|
|`docker stop <container>`|Stop container|
|`docker start <container>`|Start stopped container|
|`docker rm <container>`|Remove container|
|`docker rmi <image>`|Remove image|

---

# 🧠 Interview Mental Model

Remember these **3 commands**:

```text
mvn package
    ↓
JAR
```

```text
docker build
    ↓
Docker Image
```

```text
docker run
    ↓
Container
```

So:

```text
Spring Boot Code
       ↓
   mvn package
       ↓
      JAR
       ↓
 docker build
       ↓
 Docker Image
       ↓
  docker run
       ↓
   Container
       ↓
 Spring Boot App
```

### Interview Answer

> **To containerize a Spring Boot application, I first build the application into a JAR using Maven or Gradle. Then I create a Dockerfile with a Java runtime image, copy the JAR into the image, expose the application port, and define the entrypoint using `java -jar`. I build the Docker image using `docker build` and create a running container using `docker run` with port mapping such as `-p 8080:8080`.**