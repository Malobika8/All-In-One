# Default Vs Concrete method

In Java, **default methods** and **concrete methods** are both methods that provide implementations, but they differ in their context and usage. Here's a breakdown of the differences:

### 1. **Default Method**  
A **default method** is a method in an interface that has a body (implementation). It was introduced in Java 8 to allow adding new methods to interfaces without breaking existing implementations.  

**Key Characteristics of Default Methods:**
- Defined in interfaces using the `default` keyword.
- Provides a way to give a default implementation for methods in interfaces.
- Can be overridden by implementing classes.
- Example:
  ```java
  interface MyInterface {
      default void display() {
          System.out.println("This is a default method");
      }
  }

  class MyClass implements MyInterface {
      // No need to override the default method unless customization is needed
  }
  ```

**Use Case:**  
To add functionality to interfaces without forcing all implementing classes to override the new method.

---

### 2. **Concrete Method**  
A **concrete method** is a method in a class that has a body (implementation). It is the standard method type in Java classes.  

**Key Characteristics of Concrete Methods:**
- Defined in regular classes (or abstract classes, though they can also have abstract methods).
- Does not use the `default` keyword (the term "concrete method" is informal; it simply refers to non-abstract methods).
- Example:
  ```java
  class MyClass {
      void display() {
          System.out.println("This is a concrete method");
      }
  }
  ```

**Use Case:**  
Used in classes to define the behavior of objects.

---

### **Key Differences:**

| Feature                 | Default Method                   | Concrete Method                  |
|-------------------------|-----------------------------------|-----------------------------------|
| **Location**            | Inside an interface              | Inside a class or abstract class |
| **Keyword**             | Requires the `default` keyword   | No special keyword needed        |
| **Purpose**             | To provide default behavior in an interface | To define behavior in a class    |
| **Overriding**          | Can be overridden by implementing classes | Can be overridden by subclasses  |
| **Inheritance Context** | Interface feature (post-Java 8)  | Class feature (always available) |

**Conclusion:**  
- **Default methods** are specific to interfaces and aim to enhance interface flexibility.
- **Concrete methods** are the standard type of method implementation in classes. 

