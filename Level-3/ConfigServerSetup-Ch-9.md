## ✅ Goal

We will:

* 🔧 Create a **Config Server**
* 📂 Create a **Git repo** (or folder) with config files
* 🧩 Create a simple **client app** (`user-service`) that fetches config from the server

---

## 🚦 Step 1: Create the Config Server

### ✅ 1.1 Create a new Spring Boot project

Use [https://start.spring.io](https://start.spring.io) with:

* Project: Maven
* Name: `config-server`
* Dependencies:

  * Spring Boot DevTools (optional)
  * **Spring Web**
  * **Spring Cloud Config Server**

👉 Or use this dependency in `pom.xml`:

```xml
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-config-server</artifactId>
</dependency>
```

Also, add the Spring Cloud BOM in `<dependencyManagement>`:

```xml
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.springframework.cloud</groupId>
      <artifactId>spring-cloud-dependencies</artifactId>
      <version>2022.0.5</version> <!-- or latest compatible -->
      <type>pom</type>
      <scope>import</scope>
    </dependency>
  </dependencies>
</dependencyManagement>
```

---

### ✅ 1.2 Add `@EnableConfigServer` in main class

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

### ✅ 1.3 application.yml of config-server

```yaml
server:
  port: 8888

spring:
  cloud:
    config:
      server:
        git:
          uri: file:///${user.home}/config-repo
          clone-on-start: true

# Optional: turn off security for now
management:
  endpoints:
    web:
      exposure:
        include: "*"
```

👉 This tells Spring to read configs from a local folder like:
`C:\Users\YourName\config-repo` or `/home/you/config-repo`

---

## 📁 Step 2: Create the Git Repo (Config Storage)

Create a new folder in your system:

```
~/config-repo/
```

Inside that folder, create a file named:

```bash
user-service.yml
```

Add some dummy properties:

```yaml
spring:
  application:
    name: user-service

custom:
  message: Hello from Config Server (dev profile)
```

✅ You can also create a `user-service-dev.yml` later for `dev` profile.

Now initialize the folder as a git repo (optional for now):

```bash
cd ~/config-repo
git init
git add .
git commit -m "Initial config"
```

---

## ▶️ Step 3: Run the Config Server

Run the config-server Spring Boot app.

Then open this in your browser to test:

```
http://localhost:8888/user-service/default
```

You should see JSON with:

```json
{
  "name": "user-service",
  "profiles": ["default"],
  "propertySources": [
    {
      "name": ".../user-service.yml",
      "source": {
        "custom.message": "Hello from Config Server (dev profile)"
      }
    }
  ]
}
```

If you see this, ✅ the config server is working!

---

## 🧩 Step 4: Create the Client App (`user-service`)

Create a new Spring Boot app:

* Name: `user-service`
* Dependencies:

  * Spring Web
  * Spring Boot Actuator
  * **Spring Cloud Config Client**

### 🔧 4.1 application.yml

```yaml
spring:
  application:
    name: user-service

  config:
    import: optional:configserver:http://localhost:8888

# Optional: to read our custom property via REST
server:
  port: 8081
```

### 🔧 4.2 Create a REST Controller

```java
@RestController
public class MessageController {

    @Value("${custom.message}")
    private String message;

    @GetMapping("/msg")
    public String getMessage() {
        return message;
    }
}
```

---

## ▶️ Step 5: Run the Client App

1. First run the **config-server**
2. Then run **user-service**

Go to:

```
http://localhost:8081/msg
```

You should see:

```
Hello from Config Server (dev profile)
```

🎉 Your `user-service` is now fetching its config **from the Config Server**!

---

## 🧠 Recap

| Part                        | What it does                              |
| --------------------------- | ----------------------------------------- |
| Config Server               | Hosts shared config files                 |
| config-repo                 | Your folder or Git repo with `.yml` files |
| Client app (`user-service`) | Fetches config from the server            |
| Port 8888                   | Default port for config server            |
| Profile support             | Works with `user-service-dev.yml` etc.    |

---
