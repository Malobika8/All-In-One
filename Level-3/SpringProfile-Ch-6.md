**Spring Profiles** — a powerful feature that helps you manage **environment-specific configuration** in a clean and structured way.

---

## 🌱 What Are Spring Profiles?

**Spring Profiles** allow you to **define different configurations** (beans, properties, etc.) for different environments like:

* `dev` (Development)
* `test` (Testing)
* `prod` (Production)
* `uat`, `staging`, etc.

Instead of manually changing code or properties between environments, you define **separate profiles** and activate the right one at runtime.

---

## 🧠 Why Use Spring Profiles?

✅ Clean separation of environment-specific logic
✅ No need to comment/uncomment beans or change config manually
✅ Supports multiple profiles at once
✅ Works with properties files, YAML, and Java config

---

## ✅ Use Cases

| Use Case                             | Example                                                         |
| ------------------------------------ | --------------------------------------------------------------- |
| Use H2 in dev, MySQL in prod         | Define one `DataSource` bean in `dev` profile and one in `prod` |
| Enable debug logs in dev only        | `logging.level.root=DEBUG` in `application-dev.properties`      |
| Change API URLs based on environment | Set different values in each profile                            |

---

## 🧾 Types of Profile Usage

### 1. 🔁 **Properties File per Profile**

Create:

* `application.properties` → common to all
* `application-dev.properties` → for dev
* `application-prod.properties` → for prod

Example:

```properties
# application-dev.properties
server.port=8081
spring.datasource.url=jdbc:h2:mem:devdb
```

```properties
# application-prod.properties
server.port=80
spring.datasource.url=jdbc:mysql://prod-db:3306/app
```

---

### 2. 🛠️ **Activate a Profile**

#### Option A: In `application.properties`

```properties
spring.profiles.active=dev
```

#### Option B: Command Line

```bash
java -jar app.jar --spring.profiles.active=prod
```

#### Option C: Environment Variable

```bash
SPRING_PROFILES_ACTIVE=prod
```

---

### 3. 🧾 YAML Format with Profile Blocks

```yaml
spring:
  profiles:
    active: dev

---
spring:
  profiles: dev
server:
  port: 8081

---
spring:
  profiles: prod
server:
  port: 80
```

---

### 4. 🧬 Profile-Specific Beans

```java
@Configuration
public class AppConfig {

    @Bean
    @Profile("dev")
    public DataSource devDataSource() {
        return new HikariDataSource(...); // H2
    }

    @Bean
    @Profile("prod")
    public DataSource prodDataSource() {
        return new HikariDataSource(...); // MySQL
    }
}
```

Only the matching bean gets loaded based on the **active profile**.

---

## 📌 Checking the Active Profile at Runtime

```java
@Autowired
Environment env;

public void checkActiveProfiles() {
    String[] profiles = env.getActiveProfiles();
    Arrays.stream(profiles).forEach(System.out::println);
}
```

---

## 🧠 Summary

| Feature                  | Description                                               |
| ------------------------ | --------------------------------------------------------- |
| `spring.profiles.active` | Controls which profile is active                          |
| Property file override   | `application-{profile}.properties` override default       |
| Bean-level control       | Use `@Profile("...")` on beans to load them conditionally |
| Where to define          | Files, environment vars, CLI args                         |

---
