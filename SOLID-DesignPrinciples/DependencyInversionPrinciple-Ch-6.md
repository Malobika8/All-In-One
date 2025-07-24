## **Dependency Inversion Principle (DIP)**

### **Definition:**

> **High-level modules** should not depend on low-level modules. Both should depend on **abstractions**.
> **Abstractions should not depend on details.** Details should depend on abstractions.

### In Simple Terms:

* Don’t let **high-level logic** (like business rules) be tightly coupled to **low-level implementations** (like database access or file systems).
* Instead, both should depend on **interfaces**.
* This keeps your code **flexible, testable, and maintainable**.

---

### 🔴 Bad Example (Violates DIP)

```java
public class MySQLDatabase {
    public void save(String data) {
        System.out.println("Saved to MySQL: " + data);
    }
}

public class DataService {
    private MySQLDatabase db = new MySQLDatabase(); // ❌ tightly coupled

    public void saveData(String data) {
        db.save(data);
    }
}
```

🔴 Problem:

* `DataService` is tightly coupled to a specific database.
* If you want to switch to MongoDB or an in-memory DB — you must **change** `DataService`.
* Also makes **unit testing** harder.

### Good Example (Follows DIP)

#### Step 1: Define an abstraction (interface)

```java
public interface Database {
    void save(String data);
}
```

#### Step 2: Implement the abstraction

```java
public class MySQLDatabase implements Database {
    public void save(String data) {
        System.out.println("Saved to MySQL: " + data);
    }
}

public class MongoDatabase implements Database {
    public void save(String data) {
        System.out.println("Saved to MongoDB: " + data);
    }
}
```

#### Step 3: High-level module depends on abstraction

```java
public class DataService {
    private final Database db;

    public DataService(Database db) { // inject abstraction
        this.db = db;
    }

    public void saveData(String data) {
        db.save(data);
    }
}
```

#### Test code

```java
public class Main {
    public static void main(String[] args) {
        Database database = new MongoDatabase(); // Easily swappable
        DataService service = new DataService(database);

        service.saveData("Hello DIP");
    }
}
```

Now:

* You can switch DB implementations without touching `DataService`
* Code is **extensible**, **testable**, and **follows DIP**

### Real-World Java/Spring Example:

| Spring Feature                       | How it supports DIP                                                                    |
| ------------------------------------ | -------------------------------------------------------------------------------------- |
| `@Autowired` / Constructor Injection | Inject abstractions instead of concrete classes                                        |
| `@Qualifier`                         | Allows choosing between multiple implementations                                       |
| Spring Data JPA                      | You inject `UserRepository` (interface), Spring provides the implementation at runtime |
| Testability                          | You can inject mock dependencies for unit tests easily                                 |

## 💬 Questions

🗣️ **Q:** What is the Dependency Inversion Principle?

✅ *High-level code should depend on abstractions, not concrete classes.*

🗣️ **Q:** How do you apply it in Java?

✅ *I define interfaces for dependencies and inject them via constructor injection. I never instantiate them using `new` inside the high-level class.*

🗣️ **Q:** How does Spring support this?

✅ *Spring’s dependency injection container wires objects based on interfaces. I inject services and repositories by their interface type.*

---

## 🔍 **Question:**

You're working on a **NotificationService** that sends messages.

Here’s the current (bad) implementation:

```java
public class EmailService {
    public void send(String message) {
        System.out.println("Email sent: " + message);
    }
}

public class NotificationService {
    private final EmailService emailService = new EmailService();

    public void notifyUser(String message) {
        emailService.send(message);
    }
}
```

### Your Tasks:

1. Does this violate the Dependency Inversion Principle?
2. If yes, why?
3. Refactor the code to **follow DIP** so that:

   * `NotificationService` depends only on an abstraction
   * You can easily switch to `SMSService`, `WhatsAppService`, etc., without modifying `NotificationService`

### Sol:

> *"It violates DIP because `NotificationService` is tightly coupled to `EmailService`."*
  - ✅ Exactly. This breaks both **flexibility** and **testability**.

> *"We should have a `Notification` interface and inject its implementation."*
  - ✅ That way, `NotificationService` can work with **any type of notifier**.

#### Step 1: Define the abstraction

```java
public interface Notifier {
    void send(String message);
}
```

#### Step 2: Implementations

```java
public class EmailService implements Notifier {
    public void send(String message) {
        System.out.println("Email sent: " + message);
    }
}

public class SMSService implements Notifier {
    public void send(String message) {
        System.out.println("SMS sent: " + message);
    }
}
```

#### Step 3: High-level module (depends on interface)

```java
public class NotificationService {
    private final Notifier notifier;

    public NotificationService(Notifier notifier) {
        this.notifier = notifier;
    }

    public void notifyUser(String message) {
        notifier.send(message);
    }
}
```

#### Step 4: Test code

```java
public class Main {
    public static void main(String[] args) {
        Notifier email = new EmailService();
        Notifier sms = new SMSService();

        NotificationService service1 = new NotificationService(email);
        service1.notifyUser("Hello via Email!");

        NotificationService service2 = new NotificationService(sms);
        service2.notifyUser("Hello via SMS!");
    }
}
```

---

## Summary:

| Principle Applied | Result                                              |
| ------------------- | ----------------------------------------------------- |
| DIP                 | `NotificationService` depends on interface, not class |
| Open/Closed         | Can add new types without changing service            |
| Testability         | Easily mock `Notifier` in unit tests                  |
| Clean Design        | Clear separation of concerns                          |

---
