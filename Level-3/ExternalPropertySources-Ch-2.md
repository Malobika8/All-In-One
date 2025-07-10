# 📂 1. External Property File Setup

* Spring Boot automatically loads `application.properties` or `application.yml` files both inside the JAR and also from external locations such as:

  * The current directory
  * A `/config` subfolder alongside your JAR ([Home][1])
* To use a custom properties file outside standard locations, you can:

  * Run the app with:

    ```bash
    java -jar app.jar --spring.config.location=classpath:/default.properties,file:./custom-config/
    ```
  * Or set `spring.config.additional-location` to layer on top of the defaults ([Home][1])
 
### ✅ What is the `/config` Subfolder?

When you run a Spring Boot application as a **JAR**, Spring Boot looks for external configuration files in the following default locations (in this order):

```
1. file:./config/           ✅ Preferred place for external config
2. file:./
3. classpath:/config/
4. classpath:/
```

So, if you have a JAR like:

```
my-app.jar
```

and a folder structure like:

```
.
├── my-app.jar
└── config/
    └── application.properties
```

Spring Boot will **automatically** load `application.properties` from that `./config/` folder — **no need to pass any special flags**!

### 🔍 Why is this `/config` Folder Important?

* Keeps **your configs outside the JAR**, making it easier to update them without rebuilding.
* Supports **environment-specific configs** like `application-dev.properties`, `application-prod.yml`, etc.
* Works seamlessly with **profiles**.
* **Overrides internal config**: If the same property exists both inside the JAR and in the external `/config` folder, the external one takes precedence.

### 📌 Example Usage

Suppose your app reads a port number from config:

**`application.properties`**

```properties
server.port=9090
```

You place this file in the `./config` directory, not inside the JAR.

Then just run:

```bash
java -jar my-app.jar
```

Spring Boot will pick up that external config automatically, and start on port 9090.

### 🧠 Quick Recap

| Feature                        | Description                                                     |
| ------------------------------ | --------------------------------------------------------------- |
| Location                       | `./config/` (same directory as your JAR)                        |
| Detected Automatically?        | ✅ Yes                                                           |
| Supports Profiles?             | ✅ Yes (`application-dev.properties`, etc.)                      |
| Overrides Internal Properties? | ✅ Yes                                                           |
| Good For                       | Runtime customization, Docker/K8s volumes, externalized secrets |

---

### ✅ When Should You Use It?

* You're deploying JARs to **different environments**, and want to avoid rebuilding.
* You want to **mount a volume** in Docker containing configuration.
* You want a **clean separation** between code and config.


---

# 2. @PropertySource for Manual Imports

* Annotate a `@Configuration` class to explicitly load files outside the classpath:

  ```java
  @Configuration
  @PropertySource("file:/path/to/my.properties")
  public class AppConfig { … }
  ```
* Useful for tightly controlled or very specific external files.

---

# 3. File System Resource Loader

* For maximum control, define a bean:

  ```java
  @Bean
  public static PropertySourcesPlaceholderConfigurer placeholderConfigurer() {
      PropertySourcesPlaceholderConfigurer p = new PropertySourcesPlaceholderConfigurer();
      p.setLocation(new FileSystemResource("conf/app.properties"));
      return p;
  }
  ```
* This bean ensures Spring reads the specified file, even outside default search paths.

---

# 4. Command-Line Overrides

* Any property passed via `--key=value` or environment variables overrides values from property files ([Stack Overflow][2]).
* Example:

  ```bash
  java -jar app.jar --server.port=9000
  ```
* Great for one-off changes or dynamic deployment configuration.

---

# 5. Order of Precedence (Highest → Lowest):

1. Command-line parameters
2. `SPRING_APPLICATION_JSON` env var
3. Java System properties (`-D`)
4. OS environment variables
5. `application-{profile}.properties` && `application.properties` in external `config/`
6. The same files packaged inside the JAR
7. Defaults defined programmatically ([Home][1])

---

# ✅ Practical Usage Patterns

| Scenario                         | How to Configure                                                          |
| -------------------------------- | ------------------------------------------------------------------------- |
| One-off external properties file | Use `spring.config.location=...` or `-Dspring.config.location=...`        |
| Add layered extra configs        | Use `spring.config.additional-location`                                   |
| Targeted file import             | Use `@PropertySource("file:...")`                                         |
| Full programmatic control        | Register `PropertySourcesPlaceholderConfigurer` with `FileSystemResource` |
| Quick override during startup    | Pass as `--key=value` or set environment variable                         |

---

# Wrap-Up

In summary, Spring Boot offers a versatile external configuration system:

* **Automatic loading** from standard directories.
* **Explicit control** through annotations or bean definitions.
* **Dynamic overrides** via command-line or environment variables.

