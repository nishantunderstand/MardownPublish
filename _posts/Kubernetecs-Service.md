

# 3. How does a Service know which Pods to use?

A Service uses **labels and selectors**.

For example, Pods may have:

```
labels:
  app: payment
```

The Service can select them using:

```
selector:
  app: payment
```

So:

```
Service
  │
  │ selector: app=payment
  ↓
┌───────────────┐
│ Pods          │
│               │
│ Pod 1         │ app=payment
│ Pod 2         │ app=payment
│ Pod 3         │ app=payment
└───────────────┘
```

The Service sends traffic to Pods matching its selector.