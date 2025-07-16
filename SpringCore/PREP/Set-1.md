# What is Inversion of Control (IoC)?

### Sol:

Inversion of Control (IoC) is a design principle where the control of creating and managing objects (beans) is inverted from the application code to the Spring framework.

Instead of manually instantiating and wiring dependencies, Spring handles:
- Object creation
- Dependency injection
- Lifecycle management

We define the what (via XML or annotations like @Component, @Bean, etc.), and Spring takes care of the how.

---

# What is the difference between BeanFactory and ApplicationContext?

### Sol:

| Feature                     | `BeanFactory`                      | `ApplicationContext` (Preferred)                 |
| --------------------------- | ---------------------------------- | ------------------------------------------------ |
| Inheritance                 | Basic IoC container                | Extends `BeanFactory`                            |
| Instantiation               | Lazy (creates bean when requested) | Eager (creates all singleton beans at startup)   |
| Internationalization (i18n) | ❌ Not supported                    | ✅ Supported                                      |
| Event Propagation           | ❌ No support                       | ✅ Supports events (e.g. `ContextRefreshedEvent`) |
| Annotation scanning         | ❌ Manual setup                     | ✅ Automatically scans components                 |
| AOP Integration             | ❌ Not integrated                   | ✅ Fully supports AOP                             |
| Environment & Profiles      | ❌ Not supported                    | ✅ Supported                                      |
| Used In                     | Simple, lightweight apps           | All modern Spring applications                   |

#### Summary:

> `ApplicationContext` is a **more powerful, feature-rich container** that builds on top of `BeanFactory`. It's what we use in almost all modern Spring applications.

#### Common Implementations:

| Implementation                       | Description                                |
| ------------------------------------ | ------------------------------------------ |
| `ClassPathXmlApplicationContext`     | Loads from XML in classpath                |
| `AnnotationConfigApplicationContext` | Loads config from `@Configuration` classes |
| `GenericWebApplicationContext`       | Used in Spring Web applications            |

---

## Creating Beans Using Annotations

In Spring, we mark classes as **beans** using stereotype annotations so the container can **auto-detect and register** them.

#### Common Annotations:

| Annotation    | Purpose                                   |
| ------------- | ----------------------------------------- |
| `@Component`  | Generic bean — base for other annotations |
| `@Service`    | Used for service layer beans              |
| `@Repository` | DAO layer; enables exception translation  |
| `@Controller` | Web MVC controller                        |

🔸 All of these are **detected via component scanning** (`@ComponentScan`).

---

# Task

* Create a class `MessageService`
* Annotate it so Spring manages it as a bean
* Print a message from its method
* Create the main method that loads it using `AnnotationConfigApplicationContext`

### Sol:

```java
@Configuration
@ComponentScan
class Main {
    public static void main(String[] args) {
        ApplicationContext context = new AnnotationConfigApplicationContext(Main.class);
        MessageService messageService = context.getBean("messageService", MessageService.class);
        messageService.print();
    }
}

@Service
public class MessageService{
    
    public void print(){
        System.out.println("Printing from message service...");
    }
}
```

---

# Task:

- Create another class called NotificationService
- Make it a @Component
- Inject it into MessageService using @Autowired
- Call a method on NotificationService from MessageService#print()

### Sol:

```
@Configuration
@ComponentScan
class Main {
    public static void main(String[] args) {
        ApplicationContext context = new AnnotationConfigApplicationContext(Main.class);
        MessageService messageService = context.getBean("messageService", MessageService.class);
        messageService.print();
    }
}

@Service
public class MessageService{
    
    @Autowired
    NotificationService notificationService;
    
    public void print(){
        notificationService.notify();
    }
}

@Component
public class NotificationService{
    public void notify(){
        System.out.println("Notified...");
    }
}
```

---

# Task:

- Create the AlertService interface.
- Implement two classes: EmailAlertService and SmsAlertService
- Use @Qualifier to inject the Email one in AlertManager
- Print “Email alert sent!” from trigger().

### Sol:

```
@Configuration
@ComponentScan
class Main {
    public static void main(String[] args) {
        ApplicationContext context = new AnnotationConfigApplicationContext(Main.class);
        AlertManager alertManager = context.getBean("alertManager", AlertManager.class);
        alertManager.alert();
    }
}

@Component
public class AlertManager{
    
    @Autowired
    @Qualifier("emailAlertService")
    AlertService alertService;
    
    public void alert(){
        alertService.trigger();
    }
}

public interface AlertService{
    public void trigger();
}

@Service
public class EmailAlertService implements AlertService{
    public void trigger(){
        System.out.println("Email alert sent!");
    }
}

@Service
public class SmsAlertService implements AlertService{
    public void trigger(){
        System.out.println("Sms alert sent!");
    }
}
```

---

# Perfect — let’s now dive into:

---

## 🔹 Step 4: `@Value` Injection in Spring

`@Value` is used to inject:

* **Static values**
* **Values from `application.properties`**
* **Default fallback values**

---

### ✅ Use Cases

| Syntax                            | Injects                                         |
| --------------------------------- | ----------------------------------------------- |
| `@Value("Hello")`                 | A static string                                 |
| `@Value("${app.greeting}")`       | Value from `application.properties`             |
| `@Value("${app.greeting:Hello}")` | Value from properties, or fallback to `"Hello"` |

---

# Task:

1. Create a `GreetingService` with:
   ```java
   private String message;
   ```
2. Create a method that prints the message.
3. Fetch this service in `Main` and call that method.

We’ll skip using a real `application.properties` file right now — instead, you can pass system properties via:

```java
System.setProperty("greeting.message", "Hello from System Property");
```

### Sol:

```
@Component
public class GreetingService {
    
    @Value("${greeting.message:Default Hello}")
    private String message;

    public void greet() {
        System.out.println(message);
    }
}

public static void main(String[] args) {
    System.setProperty("greeting.message", "Hello from System Property");

    ApplicationContext context = new AnnotationConfigApplicationContext(Main.class);
    GreetingService service = context.getBean(GreetingService.class);
    service.greet();
}
```

---






