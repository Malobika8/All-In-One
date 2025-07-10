**Live reload (dynamic config refresh)** using `/actuator/refresh` so we can:

> 🔄 Update our config files →
> 🔥 Call `/actuator/refresh` →
> 💥 Changes apply **without restarting the app**

This is a powerful feature in Spring Cloud Config + Actuator + Spring Boot.

---

## ✅ Overview: What We’ll Do

1. Enable Spring Boot Actuator in your **client app** (e.g., `user-service`)
2. Add `spring-boot-starter-actuator` and `spring-cloud-starter-bootstrap`
3. Use `@RefreshScope` on the bean reading the config
4. Hit `/actuator/refresh` to reload changes from Config Server

---

## 🧱 Step-by-Step Setup

---

### ✅ 1. Add Dependencies to `user-service` (Maven)

```xml
<!-- Actuator -->
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>

<!-- Spring Cloud Starter for Config + Refresh Scope -->
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-starter-bootstrap</artifactId>
</dependency>
```

> `spring-cloud-starter-bootstrap` is required for `@RefreshScope` to work properly.

Also ensure you’re using Spring Cloud BOM:

```xml
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.springframework.cloud</groupId>
      <artifactId>spring-cloud-dependencies</artifactId>
      <version>2022.0.5</version>
      <type>pom</type>
      <scope>import</scope>
    </dependency>
  </dependencies>
</dependencyManagement>
```

---

### ✅ 2. Update `application.yml` in `user-service`

```yaml
spring:
  application:
    name: user-service

  config:
    import: optional:configserver:http://localhost:8888

  profiles:
    active: dev

management:
  endpoints:
    web:
      exposure:
        include: refresh, health, info, configprops, env

server:
  port: 8081
```

---

### ✅ 3. Use `@RefreshScope` on the bean

```java
import org.springframework.beans.factory.annotation.Value;
import org.springframework.cloud.context.config.annotation.RefreshScope;
import org.springframework.web.bind.annotation.*;

@RestController
@RefreshScope  // 🔁 IMPORTANT: enables dynamic refresh
public class MessageController {

    @Value("${custom.message}")
    private String message;

    @Value("${custom.welcome:Default welcome}")
    private String welcome;

    @GetMapping("/msg")
    public String getMessage() {
        return message + " | " + welcome;
    }
}
```

---

## ▶️ 4. Run and Test It

### 🧪 Step A: Run `config-server` and `user-service`

* Ensure both are running
* Hit:

  ```
  http://localhost:8081/msg
  ```

You’ll see the message from `user-service-dev.yml`.

---

### 🧪 Step B: Change the Config

Go to your config repo → `user-service-dev.yml`
Update the value:

```yaml
custom:
  message: Updated at runtime!
```

Commit it if you’re using Git (optional):

```bash
git add .
git commit -m "Updated message"
```

---

### 🧪 Step C: Trigger Refresh

Now make a **POST** request to:

```
http://localhost:8081/actuator/refresh
```

Use Postman or curl:

```bash
curl -X POST http://localhost:8081/actuator/refresh
```

If successful, you’ll get:

```json
["custom.message"]
```

Now refresh:

```
http://localhost:8081/msg
```

✅ You’ll see:

```
Updated at runtime! | Welcome to Dev Environment!
```

---

## 🧠 Recap

| Step                  | Description                         |
| --------------------- | ----------------------------------- |
| `@RefreshScope`       | Enables runtime refresh of beans    |
| `/actuator/refresh`   | Triggers refresh from config server |
| No app restart needed | ✅ Yes!                              |

---

## ⚠️ Important Notes

| Tip                         | Reason                                        |
| --------------------------- | --------------------------------------------- |
| `@RefreshScope` is required | Without it, changes won’t reflect             |
| POST to `/actuator/refresh` | Only a POST request triggers reload           |
| Only annotated beans update | Beans not using `@RefreshScope` won’t refresh |

---

