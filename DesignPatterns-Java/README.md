1. **Builder Pattern**

   * Purpose: Build complex objects step by step.
   * Examples: `ResponseEntity.builder()` in Spring, Lombok `@Builder`.

2. **Singleton Pattern**

   * Purpose: Ensure only one instance of a class exists.
   * Examples: Spring Beans (default singleton scope), `Runtime.getRuntime()`.

3. **Iterator Pattern**

   * Purpose: Provide a way to access elements sequentially without exposing internal structure.
   * Examples: Using `Iterator` with collections (`List`, `Set`, `Map`).

4. **Factory Pattern**

   * Purpose: Create objects without exposing instantiation logic.
   * Examples: `LoggerFactory.getLogger()`, `BeanFactory` in Spring.

5. **Observer Pattern**

   * Purpose: Notify multiple objects about a change in another object.
   * Examples: `ApplicationEventPublisher` in Spring, listeners in GUIs.

6. **Strategy Pattern**

   * Purpose: Define a family of algorithms, encapsulate each one, and make them interchangeable.
   * Examples: `Comparator` in sorting, Spring’s `PaymentStrategy` or `AuthenticationProvider`.

7. **Proxy Pattern**

   * Purpose: Provide a surrogate or placeholder to control access to an object.
   * Examples: Spring AOP proxies, Hibernate lazy-loading proxies.

8. **Decorator Pattern**

   * Purpose: Add behavior to an object dynamically without modifying its structure.
   * Examples: `BufferedReader` wraps a `Reader`, Spring `ResponseBodyAdvice`.

---

