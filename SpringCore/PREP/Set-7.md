# What are the 3 different ways to define custom init and destroy logic for Spring beans?

### Sol:

| Method                         | Init Hook                                               | Destroy Hook                          | Notes                                                |
| ------------------------------ | ------------------------------------------------------- | ------------------------------------- | ---------------------------------------------------- |
| **1. Annotations**             | `@PostConstruct`                                        | `@PreDestroy`                         | Cleanest & preferred for most use cases              |
| **2. @Bean attributes**        | `@Bean(initMethod = "init", destroyMethod = "cleanup")` | `same`                                | No need for annotations inside the method            |
| **3. Implementing interfaces** | `afterPropertiesSet()` *(from `InitializingBean`)*      | `destroy()` *(from `DisposableBean`)* | Tight coupling with Spring — not preferred for POJOs |

Using @PostConstruct and @PreDestroy is preferred because it keeps the class independent of Spring-specific interfaces. Use @Bean(initMethod, destroyMethod) when you configure beans via @Configuration.

---

# Can you write a Spring component that:
- Uses @PostConstruct to print Startup complete
- Uses @PreDestroy to print Shutting down
- Add a method called process() which is called manually in the main class

### Sol:

```
@Component
public class Test {

    @PostConstruct
    public void init() {
        System.out.println("Startup complete");
    }

    public void process() {
        System.out.println("processing...");
    }

    @PreDestroy
    public void destroy() {
        System.out.println("Shutting down");
    }
}
```
```
@Configuration
@ComponentScan(basePackages = "com.example") // Change as per your package
public class Main {

    public static void main(String[] args) {
        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(Main.class);

        Test test = context.getBean(Test.class);
        test.process();

        context.registerShutdownHook(); // Ensures @PreDestroy is called
    }
}
```

---

# Try the same using @Bean(initMethod, destroyMethod).

### Sol:

```
public class Main {
    public static void main(String[] args) {
        ConfigurableApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);

        Test test = context.getBean(Test.class);
        test.process();

        context.close(); // Calls destroy()
    }
}
```
```
@Configuration
public class AppConfig {

    @Bean(initMethod = "init", destroyMethod = "destroy")
    public Test test() {
        return new Test();
    }
}
```
```
public class Test {

    public void init() {
        System.out.println("Startup complete");
    }

    public void process() {
        System.out.println("processing...");
    }

    public void destroy() {
        System.out.println("Shutting down");
    }
}
```

---

