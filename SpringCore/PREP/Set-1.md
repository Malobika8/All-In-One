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

# 


