`@ConfigurationProperties` is one of the most powerful and cleanest ways to **bind external configuration (from properties/yaml files) into strongly-typed Java objects**.

---

## 📦 What is `@ConfigurationProperties`?

`@ConfigurationProperties` is an annotation that tells Spring Boot to:

> “Take the values from a `properties` or `yaml` file, and bind them to a Java POJO (bean).”

---

## 🧠 Why Use It?

* ✅ **Type-safe configuration**
* ✅ **Organized, hierarchical structure**
* ✅ **Supports validation with JSR-303 (e.g., `@NotNull`)**
* ✅ Works great with YAML nested structures

---

## 🔧 Basic Example

### 1. `application.properties`:

```properties
app.name=SaveNotesApp
app.version=1.0.3
```

### 2. Java POJO:

```java
@Component
@ConfigurationProperties(prefix = "app")
public class AppProperties {
    private String name;
    private String version;

    // getters and setters
}
```

➡️ Spring will bind:

* `app.name` → `AppProperties.name`
* `app.version` → `AppProperties.version`

You can then inject `AppProperties` anywhere in your app using `@Autowired`.

---

## 📚 YAML Example with Nested Properties

### `application.yml`

```yaml
server:
  port: 8080

app:
  name: SaveNotesApp
  feature:
    login-enabled: true
    max-users: 100
```

### Java class:

```java
@Component
@ConfigurationProperties(prefix = "app")
public class AppProperties {
    private String name;
    private Feature feature;

    public static class Feature {
        private boolean loginEnabled;
        private int maxUsers;

        // getters and setters
    }

    // getters and setters
}
```

---

## ✅ Enabling `@ConfigurationProperties`

Since Spring Boot 2.2+, if your class is annotated with `@Component`, nothing else is needed.

If you’re **not** using `@Component`, you must register the class manually:

### With `@EnableConfigurationProperties`

```java
@Configuration
@EnableConfigurationProperties(AppProperties.class)
public class AppConfig {
}
```

Then your POJO doesn’t need `@Component`.

---

## 🧪 Validation Support

Add validation annotations to your POJO and use `@Validated`:

```java
@Component
@ConfigurationProperties(prefix = "app")
@Validated
public class AppProperties {
    @NotNull
    private String name;

    @Min(1)
    private int version;

    // getters and setters
}
```

---

## ⚖️ Difference vs `@Value`

| Feature                      | `@ConfigurationProperties` | `@Value`                         |
| ---------------------------- | -------------------------- | -------------------------------- |
| Binding entire POJO          | ✅ Yes                      | ❌ No                             |
| Type-safe                    | ✅ Yes                      | ❌ Minimal                        |
| Hierarchical/nested support  | ✅ Yes                      | ❌ No                             |
| Supports validation          | ✅ Yes (`@Validated`)       | ❌ No                             |
| Great for many related props | ✅ Yes                      | ❌ Tedious                        |
| Best for one-off values      | ❌ Overkill                 | ✅ Yes (`@Value("${some.prop}")`) |

---

## 🔁 Summary

* Use `@ConfigurationProperties` when:

  * You have multiple related properties (especially nested)
  * You want clean, reusable configuration classes
  * You want built-in validation

---

