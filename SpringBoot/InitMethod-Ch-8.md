In Spring (both with XML and Java-based configurations), you can specify **`init-method`** in multiple ways to perform initialization logic after the bean is constructed but before it is used.

Here are the **different ways to set/init a method** in Spring:

---

### ✅ 1. **Using `@PostConstruct` Annotation (Recommended, Modern)**

* Runs after dependency injection is done.

```java
@Component
public class MyBean {

    @PostConstruct
    public void init() {
        System.out.println("Init method via @PostConstruct");
    }
}
```

✅ **Works with:**

* Java-based config
* Component scanning

📌 Requires `javax.annotation-api` or `jakarta.annotation` (depending on Spring version).

---

### ✅ 2. **Using `InitializingBean` Interface**

* Implement `afterPropertiesSet()` method.

```java
@Component
public class MyBean implements InitializingBean {
    @Override
    public void afterPropertiesSet() {
        System.out.println("Init method via InitializingBean");
    }
}
```

✅ Pros: No extra annotation needed.
🚫 Cons: Tightly couples your class with Spring.

---

### ✅ 3. **Using `initMethod` Attribute in `@Bean` (Java Config)**

* Explicitly specify which method should be called.

```java
@Configuration
public class AppConfig {
    @Bean(initMethod = "init")
    public MyBean myBean() {
        return new MyBean();
    }
}
```

```java
public class MyBean {
    public void init() {
        System.out.println("Init method via @Bean(initMethod)");
    }
}
```

---

### ✅ 4. **Using `init-method` Attribute in XML Configuration**

```xml
<bean id="myBean" class="com.example.MyBean" init-method="init"/>
```

```java
public class MyBean {
    public void init() {
        System.out.println("Init method via XML init-method");
    }
}
```

---

### 🆚 Summary Table

| Method                   | Type        | Spring-Specific? | Recommended? | Notes                   |
| ------------------------ | ----------- | ---------------- | ------------ | ----------------------- |
| `@PostConstruct`         | Annotation  | No               | ✅ Yes        | Clean and preferred way |
| `InitializingBean`       | Interface   | Yes              | 🚫 No        | Avoid tight coupling    |
| `@Bean(initMethod = "")` | Java Config | Yes              | ✅ Yes        | Explicit, flexible      |
| `init-method` (XML)      | XML Config  | Yes              | 🚫 Less used | Legacy configs          |

---

# FYI

### @PostConstruct > InitializingBean > @Bean(initMethod = "")
