## Single Responsibility Principle (SRP)

### ✅ Definition:

> A class should have **only one reason to change**.

This means: A class should **do one thing**, and **only one thing**.

---

### ❌ Bad Example: (Violates SRP)

```java
public class ReportService {
    public String generateReport() {
        // logic to generate report
        return "Report";
    }

    public void saveToFile(String content) {
        // logic to write report to file
    }

    public void sendEmail(String content) {
        // logic to send report via email
    }
}
```

🔴 Problem:

* One class handles **3 responsibilities**:

  * Business logic (generate report)
  * File I/O
  * Email sending

So, it has **3 reasons to change**:

* If report generation changes
* If file saving changes
* If email sending changes

---

### ✅ Good Example (Follows SRP)

```java
public class ReportGenerator {
    public String generate() {
        return "Report";
    }
}

public class FileSaver {
    public void save(String content) {
        // Save to file
    }
}

public class EmailSender {
    public void send(String content) {
        // Send email
    }
}
```

Now:

* Each class has **only one job**
* Each class changes for **one reason only**

---

### 🧠 Why It Matters:

✅ Makes code:

* Easier to understand
* Easier to test
* Easier to reuse
* More maintainable

---

### 💬 Questions:

🗣️ **Q:** What is SRP?

* It means a class should only do one thing and have one reason to change.

🗣️ **Q:** How do you apply it in real projects?

* I break responsibilities across services/components. For example, a class that processes payments doesn’t send emails — I use a separate notification service.

🗣️ **Q:** How does Spring encourage SRP?

* By encouraging the use of multiple `@Service`, `@Component`, `@Repository` classes — each focused on one job.

## 🔍 **Question:**

You are designing a `UserService` class that handles:

1. User registration
2. Password validation
3. Sending welcome emails

Here’s an initial version of the code:

```java
public class UserService {

    public void register(String username, String password) {
        if (isValidPassword(password)) {
            // Save user to DB
            System.out.println("User registered: " + username);
            sendWelcomeEmail(username);
        }
    }

    private boolean isValidPassword(String password) {
        return password.length() >= 8;
    }

    private void sendWelcomeEmail(String username) {
        // Email logic
        System.out.println("Welcome email sent to " + username);
    }
}
```

### 🧠 **Task:**

* Does this violate SRP?
* If yes, **refactor** it to follow SRP.
* You may use 2–3 classes if needed.

### Sol:

Each of the following concerns should be isolated:

| Responsibility      | Suggested Class                                |
| ------------------- | ---------------------------------------------- |
| Register user       | `UserRegistrationService` or `UserService`     |
| Password validation | `PasswordValidator` |
| Email notifications | `NotificationService` or `EmailService`        |

```java
public class UserRegistrationService {
    private final PasswordValidator passwordValidator;
    private final NotificationService notificationService;

    public UserRegistrationService(PasswordValidator validator, NotificationService notifier) {
        this.passwordValidator = validator;
        this.notificationService = notifier;
    }

    public void register(String username, String password) {
        if (passwordValidator.isValid(password)) {
            // Save user to DB (assume simulated here)
            System.out.println("User registered: " + username);
            notificationService.sendWelcomeEmail(username);
        }
    }
}
```

```java
public class PasswordValidator {
    public boolean isValid(String password) {
        return password.length() >= 8;
    }
}
```

```java
public class NotificationService {
    public void sendWelcomeEmail(String username) {
        System.out.println("Welcome email sent to " + username);
    }
}
```

### Optional test:

```java
public class Main {
    public static void main(String[] args) {
        PasswordValidator validator = new PasswordValidator();
        NotificationService notifier = new NotificationService();
        UserRegistrationService registrationService = new UserRegistrationService(validator, notifier);

        registrationService.register("malobika", "strongpass123");
    }
}
```

---
