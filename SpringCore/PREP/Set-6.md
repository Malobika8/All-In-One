# What is the difference between: BeanFactoryPostProcessor & BeanPostProcessor
- When in the lifecycle they are triggered
- What they can modify

### Sol:

#### ✅ Spring Bean Lifecycle with PostProcessors

```
1. Load Configuration (XML / @Configuration)
2. Load Bean Definitions (metadata)
3. 🔧 BeanFactoryPostProcessor is triggered
4. Instantiate Bean (via Constructor)
5. Inject Dependencies (Autowired, etc.)
6. 🔄 BeanPostProcessor (before initialization)
7. Call @PostConstruct / init-method / InitializingBean
8. 🔄 BeanPostProcessor (after initialization)
9. Bean is Ready to Use
```

#### ✅ 1. `BeanFactoryPostProcessor`

* 🔄 **Called before beans are instantiated**
* Operates on **Bean Definitions**, not actual beans
* Can **modify metadata**, like:

  * Change scope
  * Change property values
  * Replace bean class, etc.

```java
@Component
public class MyFactoryPostProcessor implements BeanFactoryPostProcessor {
    public void postProcessBeanFactory(ConfigurableListableBeanFactory factory) {
        BeanDefinition bd = factory.getBeanDefinition("myBean");
        bd.setScope("prototype");
    }
}
```

---

#### ✅ 2. `BeanPostProcessor`

* 🔄 **Called after a bean is instantiated and dependencies injected**
* Lets you wrap or modify the **actual bean instance**
* Two methods:

  * `postProcessBeforeInitialization()`
  * `postProcessAfterInitialization()`

```java
@Component
public class MyBeanPostProcessor implements BeanPostProcessor {
    public Object postProcessBeforeInitialization(Object bean, String name) {
        // logic here
        return bean;
    }

    public Object postProcessAfterInitialization(Object bean, String name) {
        // wrap proxy, inject logic, etc.
        return bean;
    }
}
```

#### Summary:

| Feature      | `BeanFactoryPostProcessor`               | `BeanPostProcessor`                             |
| ------------ | ---------------------------------------- | ----------------------------------------------- |
| Triggered On | **Bean definition metadata**             | **Actual bean instance**                        |
| Trigger Time | Before beans are created                 | After bean instantiation & dependency injection |
| Access to    | `BeanDefinition`                         | Actual bean object                              |
| Use Case     | Modify config, change scopes, properties | Wrap bean in proxy, logging, validation, AOP    |

#### Real Use Case:

* Spring internally uses `BeanPostProcessor` for **`@Autowired`**, **`@Transactional`**, **AOP**, etc.
* Spring uses `BeanFactoryPostProcessor` to process **`@PropertySource`**, **`@ComponentScan`**, etc.

---

# Can you write a simple `BeanPostProcessor` that logs the name of each bean after initialization?

### Sol:

```
@Component
public class Test implements BeanPostProcessor {

    @Override
    public Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
        System.out.println("Bean initialized: " + beanName);
        return bean;
    }
}
```

---

# How can we apply common logging logic

### Sol:

Let’s create a simple example where:

* We log the class name of each bean after it’s initialized
* We'll do it only for beans in a specific package (e.g. `com.app.service`)

```java
@Component
public class LoggingBeanPostProcessor implements BeanPostProcessor {

    @Override
    public Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
        if (bean.getClass().getPackageName().startsWith("com.app.service")) {
            System.out.println("[LOG] Initialized bean: " + beanName + " of type " + bean.getClass().getSimpleName());
        }
        return bean;
    }
}
```

#### Output on Startup:

```
[LOG] Initialized bean: userService of type UserService
[LOG] Initialized bean: orderService of type OrderService
```

> “Spring uses `BeanPostProcessor` behind the scenes to inject behavior into your beans. I can also write my own processor to add logging, wrap beans in custom proxies, or perform validations.”

---

# What are these annotations for - @DependsOn, @Primary, @Lazy

### Sol:

### PART 1: `@DependsOn`

#### Purpose:

Force Spring to initialize **some other bean(s) before** the current bean — even if there's no direct dependency.

#### Example:

```java
@Component("loggerService")
public class LoggerService {
    public LoggerService() {
        System.out.println("LoggerService initialized");
    }
}

@Component("userService")
@DependsOn("loggerService")
public class UserService {
    public UserService() {
        System.out.println("UserService initialized");
    }
}
```

🧠 **Output on startup:**

```
LoggerService initialized  
UserService initialized
```

Even if `UserService` does not `@Autowired` `LoggerService`, Spring ensures **LoggerService is ready first**.

### PART 2: `@Lazy`

#### Purpose:

Prevent a bean from being created at application startup (default in Spring is eager for singletons).
It will be created **only when actually needed**.

#### Example 1: On a bean

```java
@Component
@Lazy
public class ReportService {
    public ReportService() {
        System.out.println("ReportService initialized");
    }
}
```

```java
@Component
public class AdminController {

    @Autowired
    private ReportService reportService; // created only when accessed
}
```

Or:

```java
@Autowired
@Lazy
private ReportService reportService;
```

🧠 Useful when:

* A bean is **expensive to create**
* It’s used only in **rare flows**

### PART 3: `@Primary`

#### Purpose:

Resolve ambiguity when **multiple beans of the same type** exist — tells Spring to **prefer one** during autowiring.

#### Example:

```java
public interface DbConnection {}

@Component
public class MysqlConnection implements DbConnection {}

@Component
@Primary
public class OracleConnection implements DbConnection {}
```

```java
@Component
public class AppService {
    
    @Autowired
    private DbConnection dbConnection;  // → OracleConnection injected
}
```

🧠 Spring will inject **OracleConnection** because it’s marked as `@Primary`.

#### Comparison Table:

| Annotation   | Purpose                                                | Used When                                      |
| ------------ | ------------------------------------------------------ | ---------------------------------------------- |
| `@DependsOn` | Control **initialization order**                       | No direct dependency but still want load order |
| `@Lazy`      | Delay bean creation until it's actually needed         | Heavy beans, optional features                 |
| `@Primary`   | Resolve conflict among **multiple beans of same type** | No explicit `@Qualifier` used                  |

---

# You're right — thank you for the reminder! 🙏
Let’s first do the **@Primary + @Qualifier** hands-on **before** we move to init/destroy.

---

# Using `@Primary` and `@Qualifier` Together

You have 3 implementations of the same interface:

```java
public interface PaymentService {
    void pay();
}
```

Create:
* `PaypalService`
* `StripeService`
* `RazorpayService` (set this one as `@Primary`)

Then:
* Autowire `PaymentService` using `@Qualifier("stripeService")` into a class named `BillingComponent`

👉 Your task:
- Write all the required Spring components using annotations.
- Show how Spring resolves which bean to inject — and how `@Qualifier` overrides `@Primary`.

### Sol:

```
public interface PaymentService {
    void pay();
}
```
```
@Component("paypalService")
public class PaypalService implements PaymentService {
    public void pay() {
        System.out.println("Paying through PayPal");
    }
}
```
```
@Component("stripeService")
public class StripeService implements PaymentService {
    public void pay() {
        System.out.println("Paying through Stripe");
    }
}
```
```
@Component("razorpayService")
@Primary
public class RazorpayService implements PaymentService {
    public void pay() {
        System.out.println("Paying through Razorpay");
    }
}
```
```
@Component
public class BillingComponent {

    @Autowired
    @Qualifier("stripeService") // 👈 Overrides @Primary
    private PaymentService paymentService;

    public void payment() {
        paymentService.pay(); // Output: Paying through Stripe
    }
}
```

If multiple beans of the same type exist, Spring uses the @Primary bean by default. However, if @Qualifier is used during injection, it overrides the primary and selects the bean with the matching name.

---


