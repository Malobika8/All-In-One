## ✅ Spring Bean Lifecycle (Step-by-Step)

1. **Spring Container Created**
2. **Bean Definitions Loaded** from configuration (`@Component`, `@Bean`, XML, etc.)
3. **`BeanFactoryPostProcessor` invoked**

   * Modifies bean definitions **before beans are instantiated**
4. **Bean Instantiated** (using constructor or factory method)
5. **Aware Interfaces Called** (if implemented)

   * `BeanNameAware`, `BeanFactoryAware`, `ApplicationContextAware`, etc.
6. **`BeanPostProcessor#postProcessBeforeInitialization`**
7. **Custom Init Hooks (in order):**

   * `@PostConstruct`
   * `InitializingBean.afterPropertiesSet()`
   * Custom init method (`@Bean(initMethod="...")`)
8. **`BeanPostProcessor#postProcessAfterInitialization`**
9. **Ready for Use**
10. **Shutdown Phase:**

    * `@PreDestroy`
    * `DisposableBean.destroy()`
    * Custom destroy method (`@Bean(destroyMethod="...")`)

---

## Spring Bean Lifecycle with PostProcessors

1. Load Configuration (XML / @Configuration)
2. Load Bean Definitions (metadata)
3. 🔧 BeanFactoryPostProcessor is triggered
4. Instantiate Bean (via Constructor)
5. Inject Dependencies (Autowired, etc.)
6. 🔄 BeanPostProcessor (before initialization)
7. Call @PostConstruct / init-method / InitializingBean
8. 🔄 BeanPostProcessor (after initialization)
9. Bean is Ready to Use

---

### 🔸 How can you hook into the lifecycle?

* Aware interfaces
* `@PostConstruct`, `@PreDestroy`
* `InitializingBean`, `DisposableBean`
* `@Bean(initMethod=…, destroyMethod=…)`
* `BeanPostProcessor`

---


https://www.geeksforgeeks.org/spring/

## Note: Check SpringBoot folder for OenAPI/Swagger-UI & Splunk related doc

# At a Glance
<img width="1026" alt="Screenshot 2024-07-07 at 10 53 23 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/be7e924a-7514-4816-a26c-9f1ec94c7a8b">

# Spring's declarative transaction support

Spring's **declarative transaction support** allows you to handle transactions in your application without writing extra code for starting, committing, or rolling back transactions explicitly. Instead, you let Spring manage it for you automatically, using **AOP (Aspect-Oriented Programming)**. 

Here’s what it means:

1. **Without Spring's declarative transactions**: You’d have to write code like this in every method that needs a transaction:
   ```java
   Transaction tx = null;
   try {
       tx = session.beginTransaction();
       // Business logic
       tx.commit();
   } catch (Exception e) {
       if (tx != null) tx.rollback();
       throw e;
   }
   ```

   This is repetitive and clutters your business logic.

2. **With Spring's declarative transactions**: You can skip writing this boilerplate code. Instead, you mark your methods with an annotation like `@Transactional` or configure transactions in XML. Spring then automatically handles the transaction management for you behind the scenes.

   Example:
   ```java
   @Transactional
   public void saveData(MyEntity entity) {
       // Just the business logic, no transaction code!
       repository.save(entity);
   }
   ```

3. **How it works**: 
   - Spring uses **AOP (Aspect-Oriented Programming)** to "wrap" your methods in a transaction management layer.
   - This wrapping (or "interceptor") starts a transaction before your method runs and commits/rolls it back after your method completes, based on whether it was successful or failed.

4. **Configuration**:
   - You can enable this by using **annotations** like `@Transactional`.
   - Or, you can configure it in an XML file if you prefer.

### Benefits:
- Your code stays clean and focused on business logic.
- You avoid writing repetitive transaction-related code.
- It's easier to manage and maintain transactions across your application. 

