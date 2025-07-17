# What is the **difference in lifecycle** between a **singleton bean** and a **prototype bean** in Spring?

* Who manages their full lifecycle?
* When are they created?
* Are destroy callbacks called automatically for both?

### Sol:

* ✅ **Singleton bean** is created **once** per container, and **shared** across requests.
* ✅ **Prototype bean** is created **every time it is requested**.
* ✅ Singleton lifecycle is **fully managed** by the IoC container.
* ✅ In web apps, container shutdown happens automatically.
* ✅ In standalone apps, you may need `context.close()` or shutdown hook.

#### Bean Lifecycle Management**

| Aspect              | Singleton                                  | Prototype                                             |
| ------------------- | ------------------------------------------ | ----------------------------------------------------- |
| **Instance Count**  | One per Spring container                   | One **per request** (`getBean`)                       |
| **Created**         | **During container startup**               | **When explicitly requested**                         |
| **Managed By**      | Fully managed by Spring (init + destroy)   | Only **initialization** managed. Destroy not managed. |
| **Destroy Called?** | ✅ Yes (via `@PreDestroy`, `destroyMethod`) | ❌ No. You must handle manually.                       |

If you register a destroy method (like `@PreDestroy`) on a prototype bean, **Spring will not call it automatically**. You need to manage destruction logic **yourself** if you use prototype scope.

---

# You're registering a `@Bean(initMethod="init", destroyMethod="cleanup")` in a `@Configuration` class. You set it as `@Scope("prototype")`.
👉 Will `init()` and `cleanup()` both be called by Spring?

### Sol:

No. if the scope is prototye, spring only takes care of initialization. Destruction should be handled manually. So init() will be called by Spring and not cleanup().
For prototype-scoped beans, Spring only manages the creation and initialization phase. Destruction is not handled by the container, so any cleanup logic must be done manually by the client code.

---

# Spring provides several bean scopes. List all available scopes in Spring. Also mention which ones are available in web-aware applications.

### Sol:

#### Non-Web Applications
(available by default)

* **`singleton`** – One instance per Spring container
* **`prototype`** – New instance every time it’s requested

#### In Web-aware Spring Applications
(available only in web-aware containers like `WebApplicationContext`):

These additional scopes are supported:

* **`request`** – One bean instance per **HTTP request**
* **`session`** – One instance per **HTTP session**
* **`application`** – One instance per **ServletContext**
* **`websocket`** – One instance per **WebSocket**

| Scope         | Available In         | Description                       |
| ------------- | -------------------- | --------------------------------- |
| `singleton`   | All (default)        | One instance per container        |
| `prototype`   | All                  | New instance per `getBean()` call |
| `request`     | Web-only             | One per HTTP request              |
| `session`     | Web-only             | One per HTTP session              |
| `application` | Web-only             | One per ServletContext            |
| `websocket`   | Web-only (Spring 4+) | One per WebSocket session         |

To use web scopes like `request` or `session`, your application context must be web-aware (`WebApplicationContext`). Otherwise, you’ll get a runtime exception.

---

# You define a bean with `@Scope("request")` and try to access it using `AnnotationConfigApplicationContext`. 👉 What will happen?

### Sol:

If we try to use @Scope("request") in a standalone app using AnnotationConfigApplicationContext, it will throw an exception at runtime, because request scope is only valid in web-aware Spring contexts like WebApplicationContext.

---

# What are the two main types of Dependency Injection supported by Spring?
- Which one is preferred by Spring Boot and why?
- Can you give short code examples for both?

### Sol:

#### 1. **Constructor Injection** ✅ *Preferred in Spring Boot*

```java
@Component
public class Vehicle {
    private final Tyre tyre;

    @Autowired
    public Vehicle(Tyre tyre) {
        this.tyre = tyre;
    }
}
```

* **Advantages**:

  * Promotes **immutability**
  * Helps with **unit testing**
  * Ensures **mandatory dependencies** are provided
  * Makes the class easy to detect missing dependencies

#### 2. **Setter Injection**

```java
@Component
public class Vehicle {
    private Tyre tyre;

    @Autowired
    public void setTyre(Tyre tyre) {
        this.tyre = tyre;
    }
}
```

* **Used when**:

  * Dependency is **optional**
  * You want to allow changing dependency later

#### 3. **Field Injection** ❌ *Not recommended*

```java
@Component
public class Vehicle {
    @Autowired
    private Tyre tyre;
}
```

* **Not recommended** because:

  * Harder to test (no way to inject manually)
  * Breaks encapsulation
  * Not clear what dependencies are required
  * 
#### Why Constructor Injection is Preferred in Spring Boot:

* Works well with **Lombok’s `@RequiredArgsConstructor`**
* **Fails fast** if dependencies are missing
* Cleaner with **`final` fields**
* Encouraged by Spring team and industry best practices

---

# If your class has only **one constructor**, do you still need to annotate it with `@Autowired`?

### Sol:

@Autowired is Optional with a Single Constructor. If a Spring bean has only one constructor, Spring automatically uses it for dependency 
injection — no need to annotate it with @Autowired. If there are multiple constructors, then you must use @Autowired to tell Spring which one to use.
Spring performs constructor-based injection automatically if there’s a single constructor. This makes code cleaner and is part of why constructor injection is preferred.

---

# You have a property app.title=GameBuster in a file called application.properties.
How would you inject it into a field using @Value? What happens if the property is missing?

### Sol:

```java
@Value("${app.title}")
private String title;
```

This injects the value of `app.title` from `application.properties`. If the property is missing, Spring will throw an **exception** at 
startup (not assign `null`), unless:

You provide a default:

```java
@Value("${app.title:defaultValue}")
private String title;
```

* If `app.title` is present → inject it
* If missing → inject `"defaultValue"`

When the property exists but has no value:

```properties
app.title=
```

In that case, the injected value will be an **empty string (`""`)**, not `null`.

---

# You want to inject the value of `app.user.age` into an `int` field using `@Value`.
What should you be careful about?
And what happens if the property is missing or not a number?

### Sol:

If app.user.age is:
- Not defined → ❌ Exception (e.g. IllegalArgumentException: Could not resolve placeholder)
- Defined but not a number (abc) → ❌ Conversion error
- Defined correctly (25) → ✅ Injected as 25

When injecting primitives like int using @Value, the property must be present and correctly formatted. If it's missing and no default is provided, Spring throws a placeholder resolution exception. If it's not a valid number, a conversion exception occurs.

---


