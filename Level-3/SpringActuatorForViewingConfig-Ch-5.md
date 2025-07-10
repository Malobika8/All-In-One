## 🔍 Spring Boot Actuator for Viewing Configuration Properties

Spring Boot Actuator provides production-ready features like **monitoring, metrics, and inspection endpoints**, and one of the most useful ones is:

> **`/actuator/configprops`** — this endpoint shows all beans that are bound to configuration properties using:

* `@ConfigurationProperties`
* `@Value`

---

### ✅ Why Use `/actuator/configprops`?

* 📋 View **all bound configuration properties**
* 🧵 Includes your **custom @ConfigurationProperties beans**
* 🔒 Can control visibility of sensitive data
* 🧪 Useful for **debugging**, validating **external config binding**

---

## 🧱 Step-by-Step Setup

---

### 1. ✅ Add Actuator Dependency (Maven)

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

---

### 2. 🛠️ Add Your Configuration in `application.yml`

```yaml
app:
  name: SaveNotesApp
  version: 1.2.3
  author:
    name: Malobika
    email: malobika@example.com
```

---

### 3. 🧾 Create a Java POJO and Bind It with `@ConfigurationProperties`

```java
@Component
@ConfigurationProperties(prefix = "app")
public class AppProperties {
    private String name;
    private String version;
    private Author author;

    public static class Author {
        private String name;
        private String email;

        // getters and setters
    }

    // getters and setters
}
```

✅ No need for `@EnableConfigurationProperties` if you use `@Component`.

---

### 4. ⚙️ Configure Actuator in `application.properties`

```properties
# Enable the configprops endpoint
management.endpoints.web.exposure.include=configprops

# Optional: Always show values (even if marked sensitive)
management.endpoint.configprops.show-values=ALWAYS
```

---

### 5. ▶️ Run and Open `/actuator/configprops`

Once your Spring Boot app is running, visit:

```
http://localhost:8080/actuator/configprops
```

---

### ✅ Example Output for Above `AppProperties` Class

```json
{
  "contexts": {
    "application": {
      "beans": {
        "appProperties": {
          "prefix": "app",
          "properties": {
            "name": "SaveNotesApp",
            "version": "1.2.3",
            "author": {
              "name": "Malobika",
              "email": "malobika@example.com"
            }
          }
        }
      }
    }
  }
}
```

✔ `appProperties` is the bean name
✔ `prefix: "app"` is defined in the annotation
✔ `properties` are values from `application.yml`

---

## 🔐 Additional Security Config (Optional)

If you're using this in production, restrict sensitive values:

```properties
# Hide values unless explicitly allowed
management.endpoint.configprops.show-values=WHEN-authorized
```

Use Spring Security to restrict access to `/actuator/**`.

---

## 🧠 Summary Table

| Step                   | What to Do                                              |
| ---------------------- | ------------------------------------------------------- |
| Add Actuator           | Add `spring-boot-starter-actuator`                      |
| Bind POJO              | Use `@ConfigurationProperties(prefix = "app")`          |
| Enable Endpoint        | `management.endpoints.web.exposure.include=configprops` |
| View Properties        | Visit `/actuator/configprops`                           |
| Nested Props Supported | ✅ Yes                                                   |
| Show Actual Values     | `management.endpoint.configprops.show-values=ALWAYS`    |

---

