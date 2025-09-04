# 🟢 Step 1 — Config Server

### 📌 What is Config Server?

* In microservices, you don’t want to hardcode configs (`application.yml`) inside each service.
* Instead, put them in a **centralized Git repo**.
* Each service fetches its config from **Config Server** at startup.

---

### 1. Create Config Server project

Go to **Spring Initializr** and generate a new project:

* **Project name:** `config-server`
* **Dependencies:**

  * `Spring Cloud Config Server`
  * `Spring Boot Actuator` (optional but useful)

---

### 2. Enable Config Server

`ConfigServerApplication.java`

```java
@SpringBootApplication
@EnableConfigServer
public class ConfigServerApplication {
    public static void main(String[] args) {
        SpringApplication.run(ConfigServerApplication.class, args);
    }
}
```

---

### 3. Application properties

`application.yml`

```yaml
server:
  port: 8888

spring:
  application:
    name: config-server

  cloud:
    config:
      server:
        git:
          uri: https://github.com/<your-username>/<your-config-repo>
          clone-on-start: true
```

👉 This means your config server will read configs from a Git repo.

---

### 4. Git repo setup

* Create a new GitHub repo, e.g. `spring-microservices-config`.
* Add a file `product-service.yml`:

```yaml
server:
  port: 8081

spring:
  application:
    name: product-service
```

* Commit & push.

---

### 5. Run & Test

Start Config Server and open in browser:

```
http://localhost:8888/product-service/default
```

✅ You should see JSON output containing the configs from Git.

---

👉 Now any microservice (like `product-service`) can fetch its configs from here.

## Quick look

<img width="946" height="811" alt="Screenshot 2025-09-04 at 12 14 40 PM" src="https://github.com/user-attachments/assets/76e0cff4-875f-45c4-9242-462db8bc6722" />
<img width="982" height="358" alt="Screenshot 2025-09-04 at 12 14 46 PM" src="https://github.com/user-attachments/assets/9fd41895-6517-4efd-8ddb-87b6dabc3c83" />
<img width="974" height="368" alt="Screenshot 2025-09-04 at 12 14 52 PM" src="https://github.com/user-attachments/assets/ec213482-16da-491f-b327-3ba24cb5ee8b" />
