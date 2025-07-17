# What are Spring profiles used for? How do you activate a specific profile, and how do you inject a bean only for a particular profile?

### Sol:

Spring Profiles allow you to:

* Define **different beans/configs** for **different environments**
* Example: dev, test, staging, prod, or mysqldb/oracledb

This helps your app **behave differently** without code changes — just by activating a profile.

```java
@Profile("mysqldb")
@Component
public class MysqlDBConnection implements DbConnection {
    public Connection getConnection() { ... }
}
```

```java
@Profile("oracledb")
@Component
public class OracleDBConnection implements DbConnection {
    public Connection getConnection() { ... }
}
```

Only one of these will be active depending on the profile.

#### Ways to Activate a Profile:

| Method                   | How                                           |
| ------------------------ | --------------------------------------------- |
| `application.properties` | `spring.profiles.active=mysqldb`              |
| Environment Variable     | `SPRING_PROFILES_ACTIVE=mysqldb`              |
| JVM argument             | `-Dspring.profiles.active=mysqldb`            |
| Programmatically         | `ConfigurableEnvironment.setActiveProfiles()` |

#### @Profile on Bean Methods

```java
@Configuration
public class AppConfig {

    @Bean
    @Profile("mysqldb")
    public DbConnection mysqlConnection() {
        return new MysqlDBConnection();
    }

    @Bean
    @Profile("oracledb")
    public DbConnection oracleConnection() {
        return new OracleDBConnection();
    }
}
```

Only the method matching the active profile will be invoked.

> “Profiles help externalize environment-specific logic and wiring. Spring only loads beans annotated with the currently active profile.”

---

# You want to **read the current active profile** inside a Spring bean (e.g., in a `@Service` class) and perform logic based on it. How can you access the active profile programmatically?

### Sol:

Spring provides the `Environment` object — it’s auto-injected and helps you read properties, profiles, etc.

#### Example:

```java
@Service
public class SomeService {

    @Autowired
    private Environment environment;

    public void printActiveProfile() {
        String[] activeProfiles = environment.getActiveProfiles();

        for (String profile : activeProfiles) {
            System.out.println("Active Profile: " + profile);
        }
    }
}
```

* `getActiveProfiles()` → Returns all **currently active** profiles
* `getDefaultProfiles()` → Returns default profiles (if none is active)

#### Real Use Case:

```java
if (Arrays.asList(environment.getActiveProfiles()).contains("dev")) {
    // Use test DB config or enable debug logging
}
```

> “You can inject the `Environment` object and use `getActiveProfiles()` to read the currently active profile inside any Spring-managed bean.”

---

# Do you know what **Aware interfaces** are in Spring? What is the use of interfaces like `BeanNameAware` or `ApplicationContextAware`?

### Sol:

Spring provides several `*Aware` interfaces that allow beans to **access Spring container internals**. These interfaces are **callback hooks** — Spring will **inject dependencies** like `BeanFactory`, `ApplicationContext`, `BeanName`, etc., into your bean **automatically**.

#### Lifecycle Position:

* **After bean instantiation**
* **After dependency injection**
* **Before `@PostConstruct` and custom init methods**

#### Common Aware Interfaces:

| Interface                 | Injected Object        | Purpose                                                                   |
| ------------------------- | ---------------------- | ------------------------------------------------------------------------- |
| `BeanNameAware`           | `String` (bean's name) | Get the name of the current bean in the container                         |
| `ApplicationContextAware` | `ApplicationContext`   | Get full access to the Spring container (get beans, publish events, etc.) |
| `BeanFactoryAware`        | `BeanFactory`          | Access bean creation logic                                                |
| `EnvironmentAware`        | `Environment`          | Access profiles, properties                                               |
| `ResourceLoaderAware`     | `ResourceLoader`       | Load files/resources dynamically                                          |

#### Example: `ApplicationContextAware`

```java
@Component
public class MyBean implements ApplicationContextAware {

    private ApplicationContext ctx;

    @Override
    public void setApplicationContext(ApplicationContext applicationContext) {
        this.ctx = applicationContext;
    }

    public void printBeanNames() {
        for (String name : ctx.getBeanDefinitionNames()) {
            System.out.println(name);
        }
    }
}
```

#### Misconception:

> *“We can change the bean name using `BeanNameAware`”* —
> **Not quite true.** You can **read** the name but not **modify** it.


> “Spring’s Aware interfaces allow beans to access low-level container features like their own name, the application context, or environment properties. These are useful when a bean needs to interact with the Spring container programmatically.”

---

# Write a simple class implementing `BeanNameAware` and print the name of the bean. Try it yourself first.

### Sol:

```
@Service
public class Test implements BeanNameAware {

    @Override
    public void setBeanName(String beanName) {
        System.out.println("My bean name is: " + beanName);
    }
}
```

This is useful when a bean wants to know how it was named by the container — for logging, debugging, or conditional logic based on its identity.






