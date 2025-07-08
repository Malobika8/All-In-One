In Spring, just like `init-method`, there are multiple ways to define a **destroy method** (cleanup logic to be run when the application context is closed or the bean is destroyed).

---

## ✅ Different Ways to Set `destroy-method` in Spring:

---

### ✅ 1. **Using `@PreDestroy` Annotation (Recommended)**

```java
@Component
public class MyBean {

    @PreDestroy
    public void cleanup() {
        System.out.println("Cleanup via @PreDestroy");
    }
}
```

📌 **Requires:** `javax.annotation.PreDestroy` or `jakarta.annotation.PreDestroy`

✅ Works with: component scanning, Java config
🚫 Doesn’t work for prototype-scoped beans

---

### ✅ 2. **Implementing `DisposableBean` Interface**

```java
@Component
public class MyBean implements DisposableBean {
    @Override
    public void destroy() {
        System.out.println("Cleanup via DisposableBean");
    }
}
```

✅ Works always
🚫 Tightly couples your class with Spring

---

### ✅ 3. **Using `@Bean(destroyMethod = "methodName")` in Java Config**

```java
@Configuration
public class AppConfig {
    @Bean(destroyMethod = "cleanup")
    public MyBean myBean() {
        return new MyBean();
    }
}
```

```java
public class MyBean {
    public void cleanup() {
        System.out.println("Cleanup via @Bean destroyMethod");
    }
}
```

✅ Flexible and decoupled

---

### ✅ 4. **Using `destroy-method` Attribute in XML Config**

```xml
<bean id="myBean" class="com.example.MyBean" destroy-method="cleanup"/>
```

```java
public class MyBean {
    public void cleanup() {
        System.out.println("Cleanup via XML destroy-method");
    }
}
```

✅ Common in legacy XML-based configurations

---

## 🆚 Comparison Table

| Method                      | Spring Specific? | Decoupled? | Recommended? | Notes            |
| --------------------------- | ---------------- | ---------- | ------------ | ---------------- |
| `@PreDestroy`               | ❌ No             | ✅ Yes      | ✅ Yes        | Clean and modern |
| `DisposableBean.destroy()`  | ✅ Yes            | 🚫 No      | 🚫 No        | Tight coupling   |
| `@Bean(destroyMethod = "")` | ✅ Yes            | ✅ Yes      | ✅ Yes        | Flexible         |
| `destroy-method` in XML     | ✅ Yes            | ✅ Yes      | 🚫 Rarely    | Legacy style     |

---

## 🔥 Notes:

* `@PreDestroy` and `DisposableBean.destroy()` **do not work** for **prototype** scoped beans.
* Spring calls destroy methods when the context is **closed** (`context.close()` or `@PreDestroy` on shutdown).
* `destroyMethod` (Java/XML) lets you clean up even third-party beans by specifying the method explicitly.

---
