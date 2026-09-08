
[[DevOpsPicture]]

Docker : Create Container
Kubernetes : Container Orchestration

What is the difference between Docker and Kubernetes?



Kubernetes is a container orchestration platform that automates deployment, scaling, networking, and management of containerized applications across a cluster of machines.


It can automatically handle:
- Container deployment
- Scaling
- Service discovery
- Load balancing
- Self-healing
- Rolling updates
- Rollbacks
- Configuration management



---


Kubernetes


```
Kubernetes Cluster
        │
        ├── Node 1
        │    ├── Pod 1
        │    │    └── Container → Application
        │    │
        │    └── Pod 2
        │         └── Container → Application
        │
        └── Node 2
             ├── Pod 3
             │    └── Container → Application
             │
             └── Pod 4
                  └── Container → Application
```


```
                 Cluster
                    │
              Deployment
                    │
               ReplicaSet
                    │
          ┌─────────┴─────────┐
          ↓                   ↓
       Node 1              Node 2
          │                   │
       Pod 1               Pod 3
       Pod 2               Pod 4
          │                   │
     Containers          Containers
```

```
Cluster
   ↓
Deployment
   ↓
ReplicaSet
   ↓
Pods
   ↓
Containers
   ↓
Application
```

|**Component**|**Role**|
|---|---|
|**Cluster**|Contains and manages Nodes|
|**Node**|Machine/VM that provides resources to run Pods|
|**Pod**|Runs one or more containers|
|**Container**|Runs your actual application|



Kubernetes Cluster
Node : A Node is basically a machine/VM that provides:
Node = The machine that runs Pods.
Pod = The unit that runs your application container(s).
Pod : A Pod runs your application container.



Pod
A Pod is the smallest deployable unit in Kubernetes.
Pod = Wrapper around one or more containers
Manages/runs one or more containers
Provides shared network/storage context


Deployment
A **Deployment manages Pods**.
Why do we need Deployment?

A Deployment is mainly used for:
1. Replica
2. Self-Healing 
3. Rolling Updates
4. Rollback



Pod vs Deployment

| Pod                                        | Deployment                           |
| ------------------------------------------ | ------------------------------------ |
| Runs container(s)                          | Manages Pods                         |
| Smallest deployable unit                   | Kubernetes controller                |
| Can contain one or more containers         | Controls desired number of Pods      |
| If Pod dies, it doesn't replace itself     | Creates replacement Pods             |
| Usually not created directly in production | Commonly used to deploy applications |



Services in Kubernetes

The important problem is that **Pod IP addresses are not permanent**.
A Service is a Kubernetes object that provides a stable network endpoint for accessing a group of Pods.
The Service provides a stable IP address and DNS name while Pods can come and go.
Service as a Stable Address
How does a Service know which Pods to use?
[[Kubernetecs-Service]]

Service provides Load Balancing
Types

Service 
│ 
├── ClusterIP 
├── NodePort 
├── LoadBalancer 
└── ExternalName


Service vs Deployment

|Deployment|Service|
|---|---|
|Manages Pods|Provides network access to Pods|
|Maintains desired replicas|Provides a stable endpoint|
|Handles rolling updates|Routes traffic|
|Handles rollbacks|Uses selectors to find Pods|
|Creates/manages ReplicaSets|Can load-balance traffic across Pods|



ReplicaSet
A **ReplicaSet** is a Kubernetes controller whose main job is to **maintain a specified number of identical Pods**.

ReplicaSet and Deployment
A **Deployment manages the ReplicaSet**, and the ReplicaSet manages the Pods.

| Object         | Main Responsibility                               |
| -------------- | ------------------------------------------------- |
| **Pod**        | Runs container(s)                                 |
| **ReplicaSet** | Maintains the desired number of Pods              |
| **Deployment** | Manages ReplicaSets and handles updates/rollbacks |


Deployment
    │
    │ manages
    ↓
ReplicaSet
    │
    │ maintains
    ↓
  Pods
    │
    │ runs
    ↓
Container


Deployment manages ReplicaSets → ReplicaSet maintains Pods → Pod runs containers.



How do you deploy a Spring Boot application in Kubernetes?

Spring Boot → JAR → Docker Image → Registry → Deployment → ReplicaSet → Pods → Service

kubectl
kubectl is the command-line tool used to communicate with and manage a Kubernetes cluster.


What happens if a Pod crashes?
Kubernetes Check Whether Pod is Managed By
1. ReplicaSet
2. Deployment 

What if None of them is managing it ? 
No-Self Healing 



Data
1. Non-Sensitive Data
2. Sensitive Data


What are ConfigMaps?
A ConfigMap is a Kubernetes object used to store non-sensitive configuration data separately from the application code and Docker image.
For Ex:
DATABASE_URL 
APP_MODE 
SERVER_PORT 
LOG_LEVEL

What are Secrets?
A Secret is a Kubernetes object used to store sensitive data.
For Ex : 
DATABASE_USERNAME 
DATABASE_PASSWORD 
API_KEY 
TOKEN


Difference between ConfigMap and Secret?

|**ConfigMap**|**Secret**|
|---|---|
|Stores non-sensitive configuration|Stores sensitive data|
|Example: `LOG_LEVEL`|Example: `PASSWORD`|
|Example: `APP_MODE`|Example: `API_KEY`|
|Not intended for confidential data|Intended for confidential data|
|Can be injected as environment variables/files|Can be injected as environment variables/files|




What is Ingress?
Ingress is a Kubernetes resource that manages external HTTP/HTTPS traffic coming into the cluster and routes it to the appropriate Service.
Think of it as a traffic router / entry point for your applications.


```
Internet
   │
   │ HTTP / HTTPS
   ↓
Ingress
   │
   ├── /users  ──→ users-service  ──→ Pods
   │
   └── /orders ──→ orders-service ──→ Pods
```



How does Kubernetes perform load balancing?
Service 


**Service load balancing** is different from **Ingress load balancing**:

|**Service**|**Ingress**|
|---|---|
|Distributes traffic to Pods|Routes external HTTP/HTTPS traffic to Services|
|Uses Pod selectors|Uses host/path rules|
|Provides a stable network endpoint|Provides an HTTP/HTTPS entry point|
|Works at the Service/networking level|Works at the HTTP routing level|


What is a Probe?
A Probe is a health check performed by Kubernetes to find out the current state of a container/application.

Types Probe
1. Liveness Probes
2. Readiness Probes

Liveness Probes
Liveness Probe checks whether the application is still alive.


Readiness Probes
Readiness Probe checks whether the application is ready to receive traffic.


|**Liveness Probe**|**Readiness Probe**|
|---|---|
|Checks whether the application is alive|Checks whether the application is ready|
|Failure → Container may be restarted|Failure → Pod is removed from Service endpoints|
|Used to detect stuck/unhealthy applications|Used to control traffic|
|**"Should I restart it?"**|**"Should I send traffic?"**|



How do you scale an application?

Types  Scaling

1. Vertical 
	1. Vertical Pod Scaling
2. Horizontal 
	1. Horizontal Node Scaling 
	2. Horizontal Pod Scaling 
3. Manual Scaling
4. Automatic Scaling — HPA
	Horizontal Pod Autoscaler (HPA)


**Horizontal Pod Autoscaler** automatically changes the number of Pods based on metrics such as CPU or memory, subject to the configured metrics and limits.


Vertical → Bigger Pod 
Horizontal → More Pods / More Nodes 
Manual → kubectl scale 
Automatic → HPA



What is a Rolling Update?
Rolling Update = Replace Pods gradually, not all at once.




How do you view logs of a Pod?
Use the `kubectl logs` command. `kubectl logs <pod-name>`
Follow Logs in Real Time : `kubectl logs -f <pod-name>`


Common troubleshooting commands
[[Kubernetes-TroubleshootingCommands]]









