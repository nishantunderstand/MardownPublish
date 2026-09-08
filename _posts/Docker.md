- Ephemeral means lasting for a very short time or fading away quickly.
- Persistence means that data or the state of a system outlives the specific program or process that created i

---


Application Deployment Evoultion 
1. Traditional Application Deployment
2. Virtualization 
3. Containzeration

Traditional Application Deployment
Initially, applications were deployed directly on a physical server.

Virtualization 
A physical machine can be divided into multiple **Virtual Machines (VMs)**.
A hypervisor creates and manages Virtual Machines.

Examples:
1. VMware
2. VirtualBox
3. Hyper-V
4. KVM

One 1 Machine You can Run Linux as well Winodw 
No OS Sharing.
"Each VM has its own Guest OS and kernel."


Containzeration  : Heavyweight VM problem.
Instead of virtualizing hardware, containers virtualize the **Operating System level**.
We Share the HOST OS Kernel 

Virtualize/isolate the application environment

For Ex : If OS is Linux
You can run different Types of Linux
	Ubuntu
	Alphenie
But You cannot run window Application


![[Docker-Container-vs-Virtual.png]]

Virtualization vs Containzeration 


| Feature        | Virtualization          | Containerization       |
| -------------- | ----------------------- | ---------------------- |
| Unit           | VM                      | Container              |
| Main idea      | Virtual computer        | Isolated application   |
| Guest OS       | ✅ Each VM               | ❌ No separate OS       |
| Kernel         | Separate kernel per VM  | Shared host kernel     |
| Overhead       | Higher                  | Lower                  |
| Startup        | Slower                  | Faster                 |
| Resource usage | More                    | Less                   |
| Isolation      | Strong                  | Lightweight            |
| Density        | Lower                   | Higher                 |
| Typical use    | Running different OSes  | Deploying applications |
| Examples       | VMware, VirtualBox, KVM | Docker, Podman         |



---


Docker


Works on My Machine (Problem Statement)
Virtual Machine

Docker
What is Docker?
Why Docker?

Docker vs Virtual Machine

Docker Engine 
Docker Engine = Mechanism that takes the blueprint and creates/runs the instance

Docker Engine Responsebility
- Pulling images
- Creating containers
- Starting/stopping containers
- Managing container lifecycle
- Managing container networks
- Managing container storage
- Building images



Docker Architecture
![[Docker-Architecture.png]]

Docker Daemon
What if Docker Daeomon Stop ???



Docker Image
Docker Container

Image: The blueprint (read-only template). 
Container: A running instance of that image.


Docker Image Tag

Tag is essentially a human-readable reference to an image.


Docker Image vs Docker Container 
Docker vs Docker Container


Docker Lifecycle
Think of the **overall journey of an application through Docker**:
Build → Store → Pull → Run → Stop → Remove
```
docker build -t my-app .
docker push my-app
docker pull my-app
docker run my-app
docker stop my-app
docker rm my-app
```

Container Lifecycle
Container lifecycle is specifically about **one container**.

![[Docker-Container-LifeCycle.png]]



.dockerignore 
Tells Docker which files/folders to exclude from the build context.


Port Mapping
==Containers are isolated from the host network by default.

-p → Port Publishing / Mapping

EXPOSE vs -p
[[Docker-Networking-4-Expose-Expose-vs-p Trap]]


docker run vs docker start



Docker Volumes
Why do we need Volumes?
Containers are disposable. Data often needs to survive.

Storage
1. Volume 
2. Bind Mount
Which Data is persisted After Container Deletetion ?

![[Docker-Data-Persitent.png]]


Volume vs Bind Mount

![[Docker-Storage.png]]

| **Aspect** | **Volume** | **Bind Mount** |
|---|---|---|
| **Managed by** | Docker | User/Host |
| **Host path** | Docker chooses | User specifies |
| **Example** | `my-data:/app/data` | `./data:/app/data` |
| **Portability** | Generally better | More dependent on host filesystem |
| **Common use** | Persistent application/database data | Development, source-code sharing |
| **Docker-managed** | ✅ | ❌ |




How do Containers Communicate?
Containers are isolated processes, but they can communicate with each other through Docker networks.

Docker Networking Basics
[[Docker-Networking-1]]
[[Docker-Networking-2]]



Docker Compose
Multi-Stage Build

How to Optimize Docker Images

Docker Hub
**Docker Hub** is a public Docker image registry/service.


Docker Registry
A **Docker Registry** is the infrastructure that stores and distributes container images.

Docker + Jenkins
Jenkins orchestrates the pipeline
Docker packages and runs the application.

Can Multiple Containers Be Created from One Image?

Troubleshooting
docker logs : View application/container logs:
docker exec
docker inspect : Shows detailed metadata/configuration.

| Command          | Question it answers          |
| ---------------- | ---------------------------- |
| `docker logs`    | **What happened?**           |
| `docker exec`    | **What's happening inside?** |
| `docker inspect` | **How is it configured?**    |
|                  |                              |



Images
	private
	public
	
Public Vs Private Registries


Image Versioning: Docker commonly uses **tags** to identify image variants/versions:



Registry Vs Repository

```
Docker Hub
    │
    └── nginx
          ├── latest
          ├── 1.23
          ├── 1.24
          └── 1.25
```



Docker Stop
1. Graceful 
2. Forceful 

| Aspect                                 | `docker stop`   | `docker kill`          |
| -------------------------------------- | --------------- | ---------------------- |
| **Behavior**                           | Graceful        | Forceful               |
| **Signal**                             | `SIGTERM` first | `SIGKILL` by default   |
| **Gives application time to cleanup?** | ✅ Yes           | ❌ No                   |
| **Use case**                           | Normal shutdown | Emergency / force stop |

docker stop my-app
docker kill my-app