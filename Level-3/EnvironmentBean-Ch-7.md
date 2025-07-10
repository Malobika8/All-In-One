The **`Environment`** object in Spring is a very powerful interface that helps you:

✅ Access active and default profiles
✅ Read property values (from properties, YAML, system env, etc.)
✅ Check if a profile is active
✅ Programmatically access or switch configurations

---

## 🌱 What is `Environment` in Spring?

`Environment` is a core **Spring Framework interface** (not specific to Spring Boot), available in any Spring application context.

It represents the current **environment** the app is running in — including:

* Profiles
* Property sources
* System variables
* Application properties/YAML

It is part of the `org.springframework.core.env` package.

---

## 🧾 Injecting Environment

```java
import org.springframework.core.env.Environment;
import org.springframework.stereotype.Component;

@Component
public class EnvLogger {

    private final Environment environment;

    public EnvLogger(Environment environment) {
        this.environment = environment;
    }

    public void logInfo() {
        System.out.println("🔧 Active Profiles:");
        for (String profile : environment.getActiveProfiles()) {
            System.out.println(" - " + profile);
        }

        System.out.println("📦 Property 'spring.application.name': " + environment.getProperty("spring.application.name"));
    }
}
```

You can use this class anywhere to:

* List active profiles
* Fetch any property value

---

## 📦 Common Methods on `Environment`

| Method                         | Description                                      |
| ------------------------------ | ------------------------------------------------ |
| `getActiveProfiles()`          | Returns all currently active profiles            |
| `getDefaultProfiles()`         | Returns the default profiles (usually `default`) |
| `getProperty("some.key")`      | Fetches a property's value                       |
| `containsProperty("some.key")` | Checks if a property exists                      |

---

## ✅ Example Usage in a Controller

```java
@RestController
public class DemoController {

    private final Environment environment;

    public DemoController(Environment environment) {
        this.environment = environment;
    }

    @GetMapping("/env")
    public String showEnv() {
        String[] profiles = environment.getActiveProfiles();
        String appName = environment.getProperty("spring.application.name");
        return "Active: " + Arrays.toString(profiles) + " | App Name: " + appName;
    }
}
```

Request to `/env` →
Output:

```
Active: [dev] | App Name: ProfileDemo
```

---

## 🧪 Bonus: Set Active Profile Programmatically (not recommended in prod)

```java
public static void main(String[] args) {
    SpringApplication app = new SpringApplication(MyApp.class);
    app.setAdditionalProfiles("dev");
    app.run(args);
}
```

This overrides the default from properties or CLI.

---

## ⚠️ Note on `Environment` vs `@Value` vs `@ConfigurationProperties`

| Feature                 | `Environment`                 | `@Value`  | `@ConfigurationProperties`       |
| ----------------------- | ----------------------------- | --------- | -------------------------------- |
| Access single property  | ✅ Yes                         | ✅ Yes     | ✅ Yes (as part of POJO)          |
| Good for multiple props | ❌ Tedious                     | ❌ Tedious | ✅ Great for grouped/nested props |
| Supports profile access | ✅ Yes (`getActiveProfiles()`) | ❌ No      | ❌ No                             |
| Type-safe binding       | ❌ No                          | ❌ No      | ✅ Yes                            |

---

## 🧠 Summary

* `Environment` is a Spring interface to:

  * Get **active/default profiles**
  * Read **properties**
  * Access **config sources**
* It's flexible, dynamic, and injectable anywhere.
* Use it when you need **programmatic access** to the environment.

---
