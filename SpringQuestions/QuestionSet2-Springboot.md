## 1. **What is Spring Boot and how is it different from the traditional Spring Framework?**
Also, mention at least 2 key features of Spring Boot.

### Sol:

> Spring Boot is an opinionated framework built on top of the Spring Framework that **simplifies application development** by handling most of the configuration and setup automatically.

---

#### ✅ Key Differences from Traditional Spring:

| Aspect                | Spring Framework                     | Spring Boot                                             |
| --------------------- | ------------------------------------ | ------------------------------------------------------- |
| Configuration         | Manual (XML/Java Config)             | Auto-configured                                         |
| Server Setup          | External server (e.g., Tomcat/Jetty) | Embedded server (Tomcat/Jetty/Undertow)                 |
| Dependency Management | Manual version compatibility         | Handled via `spring-boot-starter-parent`                |
| App Startup           | Requires XML/web.xml setup           | Just run the `main()` method (`@SpringBootApplication`) |

#### ✅ Key Features of Spring Boot:

1. **Auto-Configuration** (`@EnableAutoConfiguration`)
2. **Starter Dependencies** (`spring-boot-starter-web`, etc.)
3. **Embedded Servers** (No need to deploy WAR to Tomcat manually)
4. **Actuator Endpoints** for monitoring
5. **Spring Boot CLI** (optional, for scripting)

---

## 2. **What does `@SpringBootApplication` do? Explain what it combines internally.**

### Sol:

`@SpringBootApplication` is a **convenience annotation** introduced by Spring Boot that combines three important annotations:

```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan
public @interface SpringBootApplication {
}
```

So it includes:

| Annotation                                        | Role                                                                                             |
| ------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| `@Configuration` (via `@SpringBootConfiguration`) | Marks the class as a source of bean definitions                                                  |
| `@EnableAutoConfiguration`                        | Triggers Spring Boot’s auto-configuration based on classpath contents                            |
| `@ComponentScan`                                  | Automatically scans the package for `@Component`, `@Service`, `@Repository`, `@Controller`, etc. |

#### 🔸 Bonus:

> **Where should you place the class annotated with `@SpringBootApplication`?**
  - It should be placed in the **root package** (or a parent package) so `@ComponentScan` can detect all components.

---

## 3. Create a minimal Spring Boot application that:

* Starts a Spring Boot app using `@SpringBootApplication`
* Has a `main()` method
* Has one REST endpoint `/ping` that returns `"pong"`

### Sol:

```java
@SpringBootApplication
public class Main {
    public static void main(String[] args) {
        SpringApplication.run(Main.class, args);
    }
}
```

```java
@RestController
public class PingController {

    @GetMapping("/ping")
    public String ping() {
        return "pong";
    }
}
```

💡 In Spring Boot:

* No XML config needed
* You can just run the app using `Main.main()` and hit `http://localhost:8080/ping`

---




