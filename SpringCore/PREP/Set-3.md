# Task:

1. Create a class `CounterService` with an `id` field.

   * Generate a random UUID or just use `System.nanoTime()` to assign it in the constructor.
   * Add a `printId()` method to print it.

2. Mark it with:

   ```java
   @Scope("prototype")
   @Component
   ```

3. In your `Main`, fetch the bean **twice** and print the ID both times.

   * If scope is `prototype` → IDs should be different
   * If scope is `singleton` → IDs should be the same

### Sol:

```
class Main {
    public static void main(String[] args) {
        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
        CounterService counterService1 = context.getBean("counterService", CounterService.class);
        counterService1.printId();
        CounterService counterService2 = context.getBean("counterService", CounterService.class);
        counterService2.printId();
        
        System.out.println(counterService1.equals(counterService2));
        context.close();
    }
}

@Configuration
@ComponentScan
public class AppConfig{

}

@Service
@Scope("prototype")
public class CounterService{
    
    private int id;
    
    CounterService(){
        this.id = System.nanoTime();
    }
    
    public void printId(){
        System.out.println("Id: " + id);
    }
}
```

---

# Task

- Create application.properties with:
  - app.name=SaveNotesApp
  - app.version=1.0.3
    
- Create AppInfoService:
  - Inject both values using @Value
  - Print them in a method printInfo()

### Sol:

```
class Main {
    public static void main(String[] args) {
        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
        AppInfoService appInfoService = context.getBean("appInfoService", AppInfoService.class);
        appInfoService.print();
    }
}

@Configuration
@ComponentScan
@PropertySource("classpath:application.properties")
public class AppConfig{

}

@Service
public class AppInfoService{
    
    @Value("${app.name}")
    private String name;
    
    @Value("${app.version}")
    private String version;
    
    public void print(){
        System.out.println("Name: " + name + " , Version: " + version);
    }
}
```

---

#### How Spring Resolves `@Value`:

Spring uses `PropertySourcesPlaceholderConfigurer` internally to replace `${...}` with values from property files.
This is triggered when you use `@PropertySource`.

#### How about injecting a default if value is missing?

```java
@Value("${app.owner:Unknown}")
private String owner;
```

---



