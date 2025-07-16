## Bean Lifecycle in Spring

Spring lets us hook into a bean’s lifecycle at two key points:

| Stage          | Annotation       | Purpose                                              |
| -------------- | ---------------- | ---------------------------------------------------- |
| Initialization | `@PostConstruct` | Runs **after** dependencies are injected             |
| Destruction    | `@PreDestroy`    | Runs **before** bean is destroyed (on context close) |

These annotations work only on **Spring-managed beans**.

### ✅ Example Flow:

```java
@Component
public class LifecycleBean {

    @PostConstruct
    public void init() {
        System.out.println("Bean initialized");
    }

    @PreDestroy
    public void cleanup() {
        System.out.println("Bean is being destroyed");
    }

    public void hello() {
        System.out.println("Hello from bean!");
    }
}
```

And in your main:

```java
AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(Main.class);
context.getBean(LifecycleBean.class).hello();
context.close();  // 🔁 Triggers @PreDestroy
```

---

# Task:

1. Create a class `PrinterService`
2. Annotate a method with `@PostConstruct` — print `"Starting printer..."`
3. Annotate another with `@PreDestroy` — print `"Shutting down printer..."`

In your `Main`:

* Get the bean from the context
* Call a method like `printStatus()`
* Then close the context to trigger `@PreDestroy`

### Sol:

```
@Configuration
@ComponentScan
class Main {
    public static void main(String[] args) {
        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(Main.class);
        PrinterService printerService = context.getBean("printerService", PrinterService.class);
        printerService.print();
        context.close();
    }
}

@Service
public class PrinterService{
    
    @PostConstruct
    public void start(){
        System.out.println("Starting printer...");
    }
    
    public void print(){
        System.out.println("Printing...");
    }
    
    @PreDestroy
    public void end(){
        System.out.println("Shutting down printer...");
    }
}
```

---

# Task:

1. Create a simple bean class `NetworkService` with:

   * `connect()` method → print `"Connecting to network..."`
   * `disconnect()` method → print `"Disconnecting from network..."`
2. In your `Main` class, register it as a bean using:

```java
@Bean(initMethod = "connect", destroyMethod = "disconnect")
public NetworkService networkService() {
    return new NetworkService();
}
```
3. Fetch it from the context and close the context.

### Sol:

```
class Main {
    public static void main(String[] args) {
        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
        NetworkService networkService = context.getBean("networkService", NetworkService.class);
        networkService.print();
        context.close();
    }
}

@Configuration
@ComponentScan
public class AppConfig{
    
    @Bean(initMethod="connect", destroyMethod="disconnect")
    public NetworkService networkService(){
        return new NetworkService();
    }
}
public class NetworkService{
    
    public void connect(){
        System.out.println("Connecting to network...");
    }
    
    public void print(){
        System.out.println("Printing...");
    }
    
    public void disconnect(){
        System.out.println("Disconnecting from network...");
    }
}
```

