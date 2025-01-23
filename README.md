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

Would you like a deeper dive into how to configure it?
