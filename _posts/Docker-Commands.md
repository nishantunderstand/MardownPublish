# Docker

docker login

How to pull/download docker Image From DockerHub ?
docker pull nginx 
docker pull nginx:1.23
if you don't mention any version, then it will install by default Latest Version.


For Checking Local Docker Images
docker images

For Checking Running Containers
docker ps

For Checking All Containers (Running & Not-Running )
docker ps -a

What does ps stand for ?
process listing


Docker Run 
1. Foreground
2. Background / Detached Mode 


How to run docker Container ?
Foreground Mode
docker run nginx:1.23

Background Mode
docker run -d nginx:1.23
docker run --detach nginx:1.23


docker run vs docker start
docker run = Create a NEW container + start it
docker start = Start an EXISTING stopped container



Download(Automatically Locally) + Run  => docker run nginx:1.22-alpine
	docker run nginx:1.22-alpine
	Unable to find image 'nginx:1.22-alpine' locally
	1.22-alpine: Pulling from library/nginx


Then how to see the logs ?
1. find docker id 
2. Then Run docker logs container-id
	docker logs 9d4895203fac

---


Learn About Standard Port Address
How to check Port Address?

- Window 
	netstat -ano | findstr :8080
	Displays network connections
	taskkill /PID 12345 /F


- Linux
	lsof -i :8080
	kill -9 4567


Lists open files (including ports)

---

How to stop a container ?
1. You need container Id  
	docker ps
2. docker stop 9d4895203fac

---

How to expose the container to my localhost ?

Port Binding

docker run -d -p 9000:80 nginx:1.23

Can we run multiple services in same port address ?
No,
Port Collision will happen

Docker run always create a new instance of docker. 
It doesn't delete old instance.

- How to preview all the instance ?
	docker ps -a
- How to run the stopped instance ?
	- docker start 2ece9ee1ce90

- Either docker is stopped by container-id or container-name
- We can give name as well.

- How to Stop Multiple Docker at once
	docker stop 9ade9b1ca3df great_sutherland

- How to assign Name 
	docker run --name web-app -d -p 9000:80 nginx:1.23
