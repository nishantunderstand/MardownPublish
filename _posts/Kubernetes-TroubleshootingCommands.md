

# Common Kubernetes Troubleshooting Commands

When a Kubernetes application has a problem, these are the most commonly used commands.

## 1. Check Pods

```bash
kubectl get pods
```

Check whether Pods are `Running`, `Pending`, `CrashLoopBackOff`, etc.

```bash
kubectl get pods -o wide
```

Shows additional information such as the Node and Pod IP.

---

## 2. Check Pod Details

```bash
kubectl describe pod <pod-name>
```

Useful for finding:

- Events
    
- Scheduling problems
    
- Container errors
    
- Probe failures
    
- Image pull problems
    

---

## 3. Check Pod Logs

```bash
kubectl logs <pod-name>
```

View application logs.

```bash
kubectl logs -f <pod-name>
```

Follow logs in real time.

```bash
kubectl logs <pod-name> --previous
```

View logs from the previous crashed container.

---

## 4. Check Deployment

```bash
kubectl get deployment
```

Check Deployment status.

```bash
kubectl describe deployment <deployment-name>
```

Get detailed Deployment information.

---

## 5. Check ReplicaSet

```bash
kubectl get replicaset
```

Check ReplicaSets and their desired/current/ready Pods.

---

## 6. Check Services

```bash
kubectl get services
```

Check available Services.

```bash
kubectl describe service <service-name>
```

Check Service details and configuration.

---

## 7. Check Nodes

```bash
kubectl get nodes
```

Check whether Nodes are `Ready`.

```bash
kubectl describe node <node-name>
```

Get detailed information about a Node.

---

## 8. Check All Resources

```bash
kubectl get all
```

Quickly view common Kubernetes resources in the current namespace.

---

## 9. Check Events

```bash
kubectl get events
```

Events are extremely useful for troubleshooting.

For example:

```text
FailedScheduling
FailedMount
Failed
BackOff
ImagePullBackOff
```

---

## 10. Execute a Command Inside a Pod

```bash
kubectl exec -it <pod-name> -- /bin/sh
```

Used to enter a running container and troubleshoot from inside it.

---

# 🧠 Troubleshooting Flow

When a Pod is not working, remember:

```text
kubectl get pods
        ↓
kubectl describe pod
        ↓
kubectl logs
        ↓
kubectl get events
        ↓
kubectl exec
```

For the overall application:

```text
Pod
 ↓
Logs / Describe
 ↓
Deployment
 ↓
ReplicaSet
 ↓
Service
 ↓
Node
```

### 🎯 Interview Answer

> **For Kubernetes troubleshooting, I commonly use `kubectl get pods` to check Pod status, `kubectl describe pod` to inspect events and configuration, `kubectl logs` to check application errors, `kubectl get events` to identify cluster events, and `kubectl exec` to troubleshoot inside a running container. I also check the Deployment, ReplicaSet, Service, and Node when necessary.**

### ⭐ Most Important Commands

```text
kubectl get pods
kubectl describe pod
kubectl logs
kubectl get events
kubectl get deployment
kubectl get replicaset
kubectl get service
kubectl get nodes
kubectl exec
```