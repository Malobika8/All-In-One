## ✅ What Are Aware Interfaces in Spring?

**Spring Aware interfaces** are used when a bean wants to be **notified of or injected with some Spring-specific infrastructure**.

They let Spring inject low-level framework objects (like `ApplicationContext`, `BeanFactory`, `BeanName`, etc.) into your bean, so the bean becomes “**aware**” of its environment.

---

## 📦 All Aware Interfaces Come from:

`org.springframework.beans.factory.Aware`

This is a **marker interface**. All other `*Aware` interfaces extend this base.

---

## ✅ Commonly Used Aware Interfaces

| Interface                 | What it makes the bean aware of         | Injected Type        |
| ------------------------- | --------------------------------------- | -------------------- |
| `BeanNameAware`           | Bean's name in the context              | `String`             |
| `BeanFactoryAware`        | The `BeanFactory` that created the bean | `BeanFactory`        |
| `ApplicationContextAware` | The `ApplicationContext`                | `ApplicationContext` |
| `EnvironmentAware`        | Environment variables/properties        | `Environment`        |
| `ResourceLoaderAware`     | Resource loading                        | `ResourceLoader`     |
| `MessageSourceAware`      | Message internationalization            | `MessageSource`      |
| `ServletContextAware`     | Web-related context (Spring MVC)        | `ServletContext`     |

---

## 🔁 How It Works Internally

1. Bean is created by Spring.
2. Spring detects that the bean implements a `*Aware` interface.
3. Spring calls the corresponding `setXxx()` method and injects the required object.

---

## ✅ Example: `ApplicationContextAware`

```java
@Component
public class MyBean implements ApplicationContextAware {
    private ApplicationContext context;

    @Override
    public void setApplicationContext(ApplicationContext ctx) {
        this.context = ctx;
        System.out.println("ApplicationContext has been set!");
    }

    public void doSomething() {
        MyService service = context.getBean(MyService.class);
        service.process();
    }
}
```

🟢 Now this bean can **dynamically access other beans** or Spring features using `ApplicationContext`.

---

## ✅ Example: `BeanNameAware`

```java
@Component
public class MyBean implements BeanNameAware {
    @Override
    public void setBeanName(String name) {
        System.out.println("My bean name is: " + name);
    }
}
```

🔎 Useful if the bean needs to behave differently based on its name.

---

## 🚫 Important Notes

* **Not recommended for regular application code** (it tightly couples your bean to Spring).
* Use dependency injection (`@Autowired`) or constructor injection **whenever possible**.
* Best used for **infrastructure components**, **custom bean factories**, or **framework features**.

---

## ✅ When Should You Use Aware Interfaces?

| Use Case                                           | Should You Use Aware?                            |
| -------------------------------------------------- | ------------------------------------------------ |
| Access another bean?                               | ❌ Use `@Autowired` instead                       |
| Access the environment (e.g., system properties)?  | ✅ Use `EnvironmentAware` or inject `Environment` |
| Need to load external resources (file, classpath)? | ✅ Use `ResourceLoaderAware`                      |
| Access context dynamically (for frameworks/tools)? | ✅ Use `ApplicationContextAware`                  |

---

## ✅ List of Common Aware Interfaces and Methods

| Interface                               | Injected Method                             |
| --------------------------------------- | ------------------------------------------- |
| `ApplicationContextAware`               | `setApplicationContext(ApplicationContext)` |
| `BeanFactoryAware`                      | `setBeanFactory(BeanFactory)`               |
| `BeanNameAware`                         | `setBeanName(String)`                       |
| `EnvironmentAware`                      | `setEnvironment(Environment)`               |
| `ResourceLoaderAware`                   | `setResourceLoader(ResourceLoader)`         |
| `MessageSourceAware`                    | `setMessageSource(MessageSource)`           |
| `ServletContextAware` (Spring MVC only) | `setServletContext(ServletContext)`         |

---

## 🔧 Behind the Scenes

Spring internally uses a `BeanPostProcessor` called:

```java
ApplicationContextAwareProcessor
```

This detects Aware interfaces and calls their `setXxx()` methods during bean initialization.

---

## 🧠 Summary

* Aware interfaces help Spring inject framework-level objects into beans.
* Use them **only when absolutely necessary**.
* Prefer standard dependency injection over `*Aware` interfaces unless you're writing **infrastructure-level code** or **custom Spring logic**.

---

## Let's walk through a simple, working example that shows how to use **`EnvironmentAware`** to read a property from the environment in a Spring Boot application.

---

## ✅ Goal

You’ll learn how to:

* Use `EnvironmentAware` to access environment properties (from `application.properties` or system environment).
* Understand how Spring injects the `Environment` into your bean.

---

## 🧩 Step-by-Step Example

### 🔹 Step 1: `application.properties`

Create this file in `src/main/resources`:

```properties
app.name=GameBuster
app.version=1.0.5
```

---

### 🔹 Step 2: Create a Bean that Implements `EnvironmentAware`

```java
import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.EnvironmentAware;
import org.springframework.core.env.Environment;
import org.springframework.stereotype.Component;

@Component
public class EnvPropertyReader implements EnvironmentAware {

    private Environment environment;

    @Override
    public void setEnvironment(Environment environment) {
        this.environment = environment;

        // Read properties manually
        String appName = environment.getProperty("app.name");
        String version = environment.getProperty("app.version");

        System.out.println("🚀 App Name from Environment: " + appName);
        System.out.println("📦 Version from Environment: " + version);
    }

    public void printOtherProps() {
        // Example of reading something else
        String javaVersion = environment.getProperty("java.version");
        System.out.println("🔧 Java Version: " + javaVersion);
    }
}
```

---

### 🔹 Step 3: Trigger It from Your Main App

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ApplicationContext;

@SpringBootApplication
public class DemoApp {
    public static void main(String[] args) {
        ApplicationContext context = SpringApplication.run(DemoApp.class, args);

        EnvPropertyReader reader = context.getBean(EnvPropertyReader.class);
        reader.printOtherProps();
    }
}
```

---

## 🧪 Output When You Run It:

```
🚀 App Name from Environment: GameBuster
📦 Version from Environment: 1.0.5
🔧 Java Version: 17.0.8
```

---

## ✅ Summary of What You Did

| What You Did                                  | How                                  |
| --------------------------------------------- | ------------------------------------ |
| Read properties from `application.properties` | Using `EnvironmentAware`             |
| Spring injected `Environment` into your bean  | Automatically via `setEnvironment()` |
| Used it like a map                            | `env.getProperty("key")`             |

---

## ✅ Alternative (Recommended for App Code)

Instead of `EnvironmentAware`, you can often use:

```java
@Value("${app.name}")
private String appName;
```

Or inject `Environment` directly:

```java
@Autowired
private Environment env;
```

But `EnvironmentAware` is helpful for:

* **Infrastructure beans**
* **Early access before DI completes**
* **Custom frameworks or logging setups**

---
