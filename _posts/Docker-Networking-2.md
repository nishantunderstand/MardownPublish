
If you're asking **“How do two Docker containers communicate?”**, the simplest mental model is:

### Container → Container

```text
┌──────────────┐        Docker Network        ┌──────────────┐
│   Backend    │ ───────────────────────────→ │  PostgreSQL  │
│  Container   │                              │  Container   │
│              │       postgres:5432          │    :5432     │
└──────────────┘                              └──────────────┘
```

### Step 1 — Create a network

```bash
docker network create app-network
```

### Step 2 — Put both containers on it

```bash
docker run -d --name backend --network app-network backend-image

docker run -d --name postgres --network app-network postgres
```

### Step 3 — Communicate using the container name

From `backend`:

```text
postgres:5432
```

For example, your Spring Boot configuration:

```properties
spring.datasource.url=jdbc:postgresql://postgres:5432/mydb
```

Docker's internal DNS resolves:

```text
postgres
   ↓
PostgreSQL container IP
```

### ⭐ Remember

```text
Container A
     │
     │ Docker Network
     ▼
Container B
```

**Same Docker network → communicate using container/service name → container port.**

And:

```text
-p 8080:8080
```

is mainly for **Host → Container** access, not required for **Container → Container** communication.