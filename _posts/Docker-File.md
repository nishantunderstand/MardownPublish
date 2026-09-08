FileName : Dockerfile
Without Extension
D should be UpperCase

docker file Structure 

docker file location

```text
Docker Tutorial/
├── Dockerfile        
├── package.json      
└── src/
    ├── server.js     
    └── (other files)
```

https://gitlab.com/twn-youtube/nginx-crash-course	

How to build docker Image ?
docker build -t node-app:1.0 .


```

Break it into 3 parts:

docker build    -t node-app:1.0    .
     │                │             │
     │                │             └── Build Context
     │                └──────────────── Image Name + Tag
     └───────────────────────────────── Build an Image


```



---

https://docs.docker.com/reference/dockerfile/

Here is the format of the Dockerfile:
```dockerfile
INSTRUCTION arguments
```
The instruction is not case-sensitive. 
However, convention is for them to be ==UPPERCASE== to distinguish them from arguments more easily.

---

https://www.youtube.com/watch?v=1ymi24PeF3M

---




FROM
RUN

WORKDIR
COPY
ADD

CMD

USER


ENV


ENTRYPOINT

EXPOSE

LABEL

SHELL You can define as powershell or cmd

Docker File Copy 
COPY vs ADD
COPY : LocalMachine
ADD : LocalMachine + RemoteLocation + Additional Feature


It define what happens when a Docker container starts.
CMD vs ENTRYPOINT
CMD : You can override Argument with run Command 
ENTRYPOINT : You Cannot 

Both Command  
1. Present
	1. How to Decide Priority  ?
	2. CMD Followed By ENTRYPOINT
	3. ENTRYPOINT Followed By  CMD
2. Absent

Either One Command Present 

ENTRYPOINT = Executable 
CMD = Default Arguments


![[Docker-CMD-Vs-EntryPoint.png]]

---


Containerize a Spring Boot Application


```dockerfile
FROM eclipse-temurin:21-jre

WORKDIR /app

COPY target/*.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]
```


How to run a Jar File ?

```
java -jar app.jar
```


How does the name get changed to app ?
```
cp target/my-app-1.0.0.jar app.jar
```



---

Build & run
```
docker build -t myapp .
docker run -p 8080:8080 myapp
```


---




Docker Image Layers 🧱
Think of a Docker image as a **stack of read-only layers**.

Layer Caching 🚀
Docker image layers are immutable/read-only.

Why Does Docker Use Layers?
The biggest reason is reuse

docker history





🔥 7️⃣ How do you reduce Java Docker image size?
✔ Use Alpine base images 
✔ Prefer JRE over JDK (if possible) 
✔ Use multi-stage builds 
✔ Copy only required files


🔥 8️⃣ What is Docker Compose?
Compose is used to run multiple containers together using a YAML file.



🔥 1️⃣3️⃣ How do you update a running container?
You cannot.
This is called immutable deployments.


Docker vs Kubernetes?
Docker → Creates & runs containers 
Kubernetes → Manages containers at scale (load balancing, auto-scaling, self-healing)

