
The short answer:

> **Because `localhost` inside a container means “this same container,” not your host machine and not another container.**

### Example

Suppose you have:

```text
┌──────────────────────┐
│ Spring Boot          │
│ Container            │
│                      │
│ localhost:3306 ❌    │
└──────────────────────┘

┌──────────────────────┐
│ MySQL Container      │
│                      │
│ :3306                │
└──────────────────────┘
```

If Spring Boot uses:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
```

Spring Boot asks:

> "Connect to MySQL on **port 3306 of THIS container**."

But MySQL is running in a **different container**.

So the connection fails. ❌

### Correct approach

Put both containers on the same Docker network:

```bash
docker network create app-network
```

```bash
docker run -d --name mysql \
  --network app-network \
  mysql
```

```bash
docker run -d --name backend \
  --network app-network \
  springboot-app
```

Now Spring Boot can connect using the **MySQL container name**:

```properties
spring.datasource.url=jdbc:mysql://mysql:3306/mydb
```

Docker's internal DNS resolves:

```text
mysql
  ↓
MySQL container IP
  ↓
port 3306
```

### Very Important Mental Model 🤔

```text
Inside Container:

localhost
   ↓
THIS container

mysql
   ↓
MySQL container

host.docker.internal
   ↓
Host machine (commonly used when connecting from container to host)
```

And remember:

> **`localhost` is relative to the process/container where the connection is made.**

### Interview-ready answer

> **A Spring Boot container cannot connect to MySQL using `localhost` when MySQL is running in another container because `localhost` refers to the Spring Boot container itself. Containers on the same Docker network should communicate using the MySQL container/service name, such as `mysql:3306`.**