
Architecuture 
1. Monolithic  : Funtion Call
2. Microservice : ServiceDiscovery

Why Service Discovery 
[https://www.instagram.com/reels/Dcz5zVxhZ4c/](https://www.instagram.com/reels/Dcz5zVxhZ4c/)


Types : 
1. Client Side Service Discovery
2. Server Side Service Discovery 
  
Kubernetes is a very common example of server-side service discovery.
  
Server Side → API Gateway + Load Balancer
Service Registry Example 👈👈👈👈👈
  


How does Eureka work? 

---

Service Discovery vs API Gateway
Service Discovery vs Load Balancer
Service Discovery vs Service Mesh

---

Heartbeat 🤔🤔🤔  Is this realted to Service Discovery ?

---

Service to Service Communication
1. Synchronous Communication : Rest Client , Feign Client , WebClient👈👈👈👈👈
2. Asynchronous Communication : Kafka 

---

ServiceDiscovery
1. Client Side 
2. Server Side👈👈👈👈👈

Service Scaling  : Load Balancer
Service Register  : Service Registry
Service Finding  : Service Discovery 
Service Communicate : 
1. Sync 
2. Async 

---



ServiceDiscovery
Why ?

ServiceDiscovery + Microservice + ScaleUp/Down

1. Client ServiceDiscovery
2. Server ServiceDiscovery

---
Service Registry👈👈👈👈👈
      ↓
Stores service locations

Service Registration👈👈👈👈👈
      ↓
Service tells registry:
"I am Payment Service at IP:Port X"

Service Discovery
      ↓
Service asks:
"Where is Payment Service?"

Load Balancing
      ↓
"Which Payment instance should I call?"

---
Service Discovery vs Service Registry

Service Mesh
Istio