# 🌩️ Spring Cloud Config Server — Full Beginner-Friendly Notes (`application.yml` + `bootstrap.yml`)

---

## 📌 What is Spring Cloud Config?

Spring Cloud Config allows you to **store all your configuration files in a central Git repository** and fetch them dynamically into your Spring Boot apps at startup.

### 🔧 Why use it?

* You no longer need to maintain individual `application.yml` files inside each microservice.
* Easy to update configurations across environments (dev, test, prod).
* No need to rebuild or redeploy services for config changes (with `/refresh` endpoint).

---

## 🔗 Key Components

| Component         | Description                                                                |
| ----------------- | -------------------------------------------------------------------------- |
| 🧾 Git Repo       | Stores external configuration files (`*.yml` or `*.properties`)            |
| 🖥️ Config Server | A Spring Boot app that reads the Git repo and serves config files via HTTP |
| 📦 Config Client  | Your microservices that fetch config values from the config server         |

---

## 🛠️ Step-by-Step Setup

---

### ✅ 1. Create a Git Repo for Config Files

Example folder structure:

```
config-repo/
├── application.yml
├── user-service.yml
└── order-service.yml
```

#### Example: `user-service.yml`

```yaml
server:
  port: 8081

custom:
  message: "Hello from Git"
```

> 📌 File name must match the `spring.application.name` of the client.

---

### ✅ 2. Create the Config Server (Spring Boot App)

#### a. Add Dependencies in `pom.xml`

```xml
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-config-server</artifactId>
</dependency>

<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

#### b. Add Spring Cloud BOM

```xml
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.springframework.cloud</groupId>
      <artifactId>spring-cloud-dependencies</artifactId>
      <version>2021.0.7</version> <!-- Use compatible version -->
      <type>pom</type>
      <scope>import</scope>
    </dependency>
  </dependencies>
</dependencyManagement>
```

#### c. Main Class

```java
@SpringBootApplication
@EnableConfigServer
public class ConfigServerApplication {
    public static void main(String[] args) {
        SpringApplication.run(ConfigServerApplication.class, args);
    }
}
```

#### d. `application.yml` (for Config Server)

```yaml
server:
  port: 8888

spring:
  cloud:
    config:
      server:
        git:
          uri: https://github.com/your-username/config-repo
          clone-on-start: true
```

> 🧪 If you're using a local folder:

```yaml
spring:
  cloud:
    config:
      server:
        git:
          uri: file:///C:/Users/yourname/config-repo
```

---

### ✅ 3. Run the Config Server

Start the server. Test it by visiting:

```
http://localhost:8888/user-service/default
```

You should see the properties in JSON format.

---

### ✅ 4. Create a Config Client (e.g., `user-service`)

#### a. Add Dependencies

```xml
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-starter-config</artifactId>
</dependency>

<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

---

### ✅ 5. Using `application.yml` (Spring Boot 2.4+)

In `src/main/resources/application.yml`:

```yaml
spring:
  application:
    name: user-service

  config:
    import: optional:configserver:http://localhost:8888

server:
  port: 8081

management:
  endpoints:
    web:
      exposure:
        include: refresh
```

> ✅ `spring.config.import` is the **new way** (2.4+) to load config server via `application.yml`.

---

### ✅ 6. Using `bootstrap.yml` (Spring Boot < 2.4 or legacy)

In `src/main/resources/bootstrap.yml`:

```yaml
spring:
  application:
    name: user-service

  cloud:
    config:
      uri: http://localhost:8888
```

In `application.yml` (keep other configs here):

```yaml
server:
  port: 8081
```

---

### ✅ 7. Access Config in Code

```java
@RestController
public class MessageController {

    @Value("${custom.message}")
    private String message;

    @GetMapping("/message")
    public String getMessage() {
        return message;
    }
}
```

Visit:

```
http://localhost:8081/message
```

Output:

```
Hello from Git
```

---

## 🔁 Optional: Refresh Without Restart

#### 1. Add actuator dependency:

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

#### 2. Expose the `/refresh` endpoint:

```yaml
management:
  endpoints:
    web:
      exposure:
        include: refresh
```

#### 3. Trigger refresh:

```bash
curl -X POST http://localhost:8081/actuator/refresh
```

---

## 🔄 `application.yml` vs `bootstrap.yml`

| Feature                    | `application.yml` (new)           | `bootstrap.yml` (legacy)          |
| -------------------------- | --------------------------------- | --------------------------------- |
| Introduced in              | Spring Boot 2.4+                  | Before 2.4                        |
| Purpose                    | Unified config, simpler structure | Separate early config loading     |
| Needed for config server?  | ✅ Yes, via `spring.config.import` | ✅ Yes, via `spring.cloud.config`  |
| Preferred for new projects | ✅ Yes                             | ❌ Only if maintaining old project |
| Loads during               | Application context phase         | Bootstrap phase                   |

---

## ✅ Summary

* ✅ Use `application.yml` + `spring.config.import` if you're using Spring Boot 2.4 or later.
* ✅ Use `bootstrap.yml` if you're on older Spring Boot or want to separate config loading.
* ✅ Always match config file name in Git to the client’s `spring.application.name`.
* ✅ Use `/actuator/refresh` to reload config without restarting the app.

---

