# What is JWT? How is it used in securing microservices? Why is it preferred over session-based auth?

### Sol:

**JWT (JSON Web Token)** is a **compact**, **URL-safe**, and **self-contained** way to transmit **claims (user identity, roles, etc.)** between two parties — typically between a **client and a server**.

#### JWT in Microservices Security

1. ✅ **Authentication Flow**:

   * The client (user) logs in with credentials (e.g., email & password).
   * The **Auth Service** validates the credentials and returns a **JWT**.
   * The client includes this JWT in the **Authorization header** of every request:

     ```
     Authorization: Bearer <token>
     ```

2. ✅ **Authorization**:

   * Microservices **decode the token** to verify:

     * Who the user is (subject)
     * What roles/permissions they have
     * Whether the token is valid or expired

3. ✅ **Stateless**:

   * No session is stored on the server — the JWT **carries all user info** in itself.
   * This is perfect for microservices, which are typically **stateless and horizontally scalable**.

---

#### Why JWT is Preferred over Session-based Auth:

| Session-Based                      | JWT-Based                                |
| ---------------------------------- | ---------------------------------------- |
| Server stores session              | Token is self-contained, no server state |
| Doesn't scale well across services | Stateless — works well in microservices  |
| Needs sticky sessions / central DB | No shared storage needed                 |

---

#### JWT Structure:

```
xxxxx.yyyyy.zzzzz
 |     |      |
 |     |      └─ Signature (used to verify the token)
 |     └──────── Payload (claims like user, role, etc.)
 └────────────── Header (alg=HS256, typ=JWT)
```

You can decode the JWT using tools like [jwt.io](https://jwt.io) to see the claims inside.

> "JWT is a stateless token used for authenticating and authorizing users across microservices by securely transmitting user claims in a compact, self-contained format."

---

# What is Spring Cloud Config Server and why do we need it in a microservices architecture?

#### Sol:

In a microservices architecture, each service usually has its own config (`application.yml`) — including things like DB URLs, credentials, feature flags, etc.

When configs are embedded in the service:

* Any config change requires **rebuild + redeploy** of the service
* Difficult to **maintain consistency** across environments (dev, QA, prod)

🔧 **Spring Cloud Config Server** solves this by:

* Acting as a **centralized configuration server**
* Reading config files from a **Git repo** (or file system, Vault, etc.)
* Serving config values to client microservices via **HTTP API**
* Allowing **dynamic updates** (with Spring Cloud Bus for live reload)

Each client microservice contacts the config server during startup (and optionally at runtime) to fetch its config.

This follows the **"12-Factor App"** principle: *Externalize configuration*.

---

# Can you describe the **steps required to set up a Spring Cloud Config Server** from scratch? Mention key annotations, dependencies, and properties.

### Sol:

#### Step 1: Create the Config Server

1. **Create a new Spring Boot project**
   Include this dependency in `pom.xml`:

   ```xml
   <dependency>
       <groupId>org.springframework.cloud</groupId>
       <artifactId>spring-cloud-config-server</artifactId>
   </dependency>
   ```

2. **Add annotation to main class**:

   ```java
   @SpringBootApplication
   @EnableConfigServer
   public class ConfigServerApplication {
       public static void main(String[] args) {
           SpringApplication.run(ConfigServerApplication.class, args);
       }
   }
   ```

3. **application.yml** in Config Server:

   ```yaml
   server:
     port: 8888

   spring:
     cloud:
       config:
         server:
           git:
             uri: https://github.com/my-org/config-repo
             default-label: main
             clone-on-start: true
   ```

#### Step 2: Create the Git Repo

Inside the Git repo (e.g., `https://github.com/my-org/config-repo`), create files like:

```
application.yml                  <-- global config for all services
student-service.yml             <-- specific config for student-service
order-service.yml               <-- for order-service
student-service-dev.yml         <-- profile-specific config
```

#### Step 3: Config Client Setup (for each microservice)

1. Add dependency in client service:

   ```xml
   <dependency>
       <groupId>org.springframework.cloud</groupId>
       <artifactId>spring-cloud-starter-config</artifactId>
   </dependency>
   ```

2. In the client’s `bootstrap.yml` (or `application.yml`):

   ```yaml
   spring:
     application:
       name: student-service
     cloud:
       config:
         uri: http://localhost:8888
   ```

   🔁 Or if using Eureka:

   ```yaml
   spring:
     cloud:
       config:
         discovery:
           enabled: true
           service-id: config-server
   ```

3. The service will then fetch its config from:

   ```
   http://localhost:8888/student-service/default
   ```

#### Optional: Dynamic Refresh with Spring Cloud Bus

* Add `spring-cloud-starter-bus-amqp` (RabbitMQ) or Kafka.
* Use `@RefreshScope` on beans to enable dynamic reloading.
* Send a POST to `/actuator/busrefresh` to broadcast the change.

> "Spring Cloud Config Server centralizes configuration in a Git repo, and client services fetch their configs during startup based on their name and profile. This helps avoid redeployments for config changes and ensures consistency across services and environments."

---

# Suppose you want `student-service` and `order-service` to share some **common configuration**, but also have **environment-specific overrides**. How would you structure this in the config repo?

### Sol:

To manage shared and environment-specific configurations using Spring Cloud Config:

#### 🔹 1. **Global Config (Common to All Services)**

📄 `application.yml`

```yaml
server:
  port: 8080

logging:
  level:
    root: INFO
```

This config is **shared** by all services (`student-service`, `order-service`, etc.)

#### 🔹 2. **Service-Specific Config (Generic Profile)**

📄 `student-service.yml`

```yaml
message: Hello from Student Service
db:
  url: jdbc:mysql://localhost:3306/student
```

📄 `order-service.yml`

```yaml
message: Hello from Order Service
db:
  url: jdbc:mysql://localhost:3306/order
```

#### 🔹 3. **Service-Specific Config by Profile**

📄 `student-service-dev.yml`

```yaml
db:
  username: dev_user
  password: dev_pass
```

📄 `order-service-prod.yml`

```yaml
db:
  username: prod_user
  password: prod_pass
```

#### How Spring Cloud Config resolves this:

When `student-service` starts in **dev** profile:

```yaml
spring:
  application:
    name: student-service
  profiles:
    active: dev
```

It fetches configs from:

```
http://<config-server>/student-service/dev
```

Spring will merge:

* `application.yml` → global
* `student-service.yml` → service-specific
* `student-service-dev.yml` → profile-specific

Later keys override earlier ones.

> "We organize shared config in `application.yml`, service-specific in `service-name.yml`, and environment overrides in `service-name-profile.yml`. Spring merges these at runtime based on active profile."

---

# Suppose you change the DB URL for `student-service` in Git. How do you make the service **pick up the new config without restarting**?

### Sol:

To update config in a running microservice without restarting:

#### 🔹 Step-by-Step:

1. ✅ **Push the new config** to the Git repo connected to your Config Server.

2. ✅ **Trigger refresh** in the client service.

   * If using plain Spring Cloud Config:

     ```bash
     POST http://localhost:8081/actuator/refresh
     ```

   * If using Spring Cloud Bus (recommended for multiple services):

     ```bash
     POST http://localhost:8081/actuator/busrefresh
     ```

   This broadcasts the refresh signal to **all services** connected via RabbitMQ or Kafka.

3. ✅ Annotate your beans with:

   ```java
   @RefreshScope
   ```

   This tells Spring that the bean should be **reloaded** when a refresh is triggered.

#### Tip:

You can monitor which properties changed by hitting:

```
GET /actuator/env
```

> "We push the config changes to Git, then trigger `/actuator/refresh` or `/busrefresh` to reload beans annotated with `@RefreshScope` without restarting the service."

---

# What happens if the Config Server is down when a microservice starts? How would you handle or prevent failure in such cases?

### Sol:

If a microservice can't reach the **Config Server** during startup:

* By default, **Spring Boot fails to start** with an error like:

  ```
  Could not locate PropertySource: I/O error on GET request for config
  ```

This is a critical issue in **cloud environments**, where network blips are common.


#### ✅ How to handle it:

#### ✅ 1. **High Availability for Config Server**

* Run **multiple instances** of the config server (e.g., behind a load balancer)
* Register them with **Eureka** (service discovery) so clients can fall back

```yaml
spring:
  cloud:
    config:
      discovery:
        enabled: true
        service-id: config-server
```

#### ✅ 2. **Fail Fast Control**

By default, clients **fail-fast** if config server is unreachable.
You can disable that:

```yaml
spring:
  cloud:
    config:
      fail-fast: false
```

This tells Spring: *If the config server is down, don’t crash — just use what you have locally.*

#### ✅ 3. **Use a Local Fallback (`bootstrap.yml`)**

You can define **essential fallback configs** inside the service’s `bootstrap.yml`:

```yaml
spring:
  application:
    name: student-service
  profiles:
    active: dev
  cloud:
    config:
      uri: http://localhost:8888
      fail-fast: false
```

This way, if the config server is down, the service **starts with minimal/default config**, and logs a warning.

> "If the config server is down, services normally fail to start.
> To prevent this, we run config servers in high availability mode, use `fail-fast=false`, and provide fallback configs in `bootstrap.yml`. This ensures the system is resilient and partially functional during outages."

---




