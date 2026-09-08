
## `EXPOSE` vs `-p`

This is a **very common Docker interview question**.

### 1. `EXPOSE`

`EXPOSE` is written inside the **Dockerfile**:

```dockerfile
EXPOSE 8080
```

It means:

> **The application inside this image is intended to listen on port 8080.**

It is mainly **metadata/documentation**. It does **not** publish the port to your host by itself.

---

### 2. `-p`

`-p` is used with `docker run`:

```bash
docker run -p 9090:8080 my-app
```

It means:

> **Map host port `9090` → container port `8080`.**

```text
Host Machine                 Container
┌──────────────┐             ┌──────────────┐
│     :9090    │ ──────────► │     :8080    │
└──────────────┘             └──────────────┘
```

Now you can access:

```text
http://localhost:9090
```

---

## Side-by-side

|`EXPOSE`|`-p`|
|---|---|
|Dockerfile instruction|`docker run` option|
|Documents container port|Publishes/maps a port|
|Does **not** create host mapping|Creates host → container mapping|
|`EXPOSE 8080`|`-p 9090:8080`|
|Optional metadata|Needed for external host access|

### Important mental model

```text
Dockerfile
    │
    └── EXPOSE 8080
          ↓
    "My app uses 8080"
    
docker run
    │
    └── -p 9090:8080
          ↓
    "Host 9090 → Container 8080"
```

### Interview trap ⚠️

If you have:

```dockerfile
EXPOSE 8080
```

and run:

```bash
docker run my-app
```

**Can you access it using `localhost:8080`?**

❌ **Not necessarily.**

You generally need:

```bash
docker run -p 8080:8080 my-app
```

### One-line interview answer

> **`EXPOSE` declares/document the port the containerized application listens on, while `-p` actually publishes a container port to a host port.**