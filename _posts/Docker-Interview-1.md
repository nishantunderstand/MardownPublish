
Docker Interview Question
 1. Why can't a Spring Boot container connect to MySQL using localhost? 
 2. If you delete a container, will your MySQL data be deleted?
 3. Can multiple containers be created from one image?
 4. Why is Docker faster than Virtual Machines?
 5. Is Docker a Virtual Machine?
 6. What happens if you modify a running container?
	 1. Will they survive restart/stop ?
	 2. What if Container is lost ?
 7. ==Can we update an Image?==
	 1. Can we modify image ?
 8. Difference between docker stop and docker kill
 9. Difference between docker run and docker start
 10. Why do we expose ports?
 11. Is EXPOSE mandatory?
 12. Difference between COPY and ADD
 13. Why use Multi-stage Build?
 14. Why use JRE instead of JDK in Production?
 15. Can Docker run without an Image? 
 16. What is the difference between Bind Mount and Volume?
 17. Can one container use multiple volumes?
 18. What is the difference between CMD and ENTRYPOINT?
 19. Why is Docker called "Lightweight"?
 20. What is Docker Compose?
 21. What happens if two containers use the same host port?
 22. Jenkins built the Docker image. Do production servers also need Maven?
 23. Why push to Docker Hub instead of copying the JAR?
 24. If Jenkins is restarted, will running Docker containers stop?
 25. Where should database passwords be stored?
 26. Difference between Dockerization and Containerization
 27. Can one Image have multiple tags?
 28. Why do we use .dockerignore?
 29. What happens if the Docker daemon stops?
 30. ==Most Asked Scenario Question , Jenkins builds your application. Explain how you would deploy it to production using Docker==
 31. Can Jenkins run inside Docker?
 32. What happens if the Jenkins build fails?
 33. ==Why use Docker agents in Jenkins?==
 34. If Docker Hub is unavailable, can you still deploy?

---


7] Can we update an Image?
Docker images are immutable. We don't modify an existing image in place; instead, we rebuild a new image from an updated Dockerfile/application.


29] What happens if the Docker daemon stops?
"If the Docker daemon stops, Docker CLI operations cannot communicate with Docker, so container management becomes unavailable. Running containers may continue depending on the configuration, such as live restore. If the daemon or host failure ultimately causes the container processes to stop, they won't be managed or restarted until Docker is available again."

30] Most Asked Scenario Question , Jenkins builds your application. Explain how you would deploy it to production using Docker

```
Developer
    │
    │ git push
    ▼
Git Repository
    │
    ▼
Jenkins
    │
    ├── 1. Checkout code
    │
    ├── 2. Run tests
    │
    ├── 3. Maven build
    │
    ├── 4. Create Docker image
    │
    ├── 5. Tag image
    │
    └── 6. Push image
            │
            ▼
       Docker Registry
            │
            │ pull
            ▼
     Production Server
            │
            ▼
      Docker Container
            │
            ▼
       Running App
```