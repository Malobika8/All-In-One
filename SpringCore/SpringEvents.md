# Brief Introduction

## ✅ What Are Spring Events?

Spring provides a **publish-subscribe** mechanism for beans to **communicate indirectly**, without tight coupling.

> 🧠 You can think of it as:
> **“Hey, something happened — whoever cares about this, react!”**

---

### ✅ Components Involved:

| Component                   | Role                               |
| --------------------------- | ---------------------------------- |
| `ApplicationEventPublisher` | Sends the event                    |
| `@EventListener`            | Listens and reacts to the event    |
| `ApplicationEvent`          | The event object (can be any POJO) |

---

### 🔁 Real-Life Analogy:

* After a user registers, you want to:

  * Send a welcome email
  * Log audit trail
  * Notify admins

Rather than calling all these directly inside the registration code, you can just **publish a `UserRegisteredEvent`** and let whoever’s interested listen for it.

---

## ✅ Minimal Code Example

### 🔹 Event Class

```java
public class UserRegisteredEvent {
    private final String username;

    public UserRegisteredEvent(String username) {
        this.username = username;
    }

    public String getUsername() {
        return username;
    }
}
```

---

### 🔹 Publisher

```java
@Component
public class UserService {

    @Autowired
    private ApplicationEventPublisher publisher;

    public void registerUser(String username) {
        System.out.println("User registered: " + username);
        publisher.publishEvent(new UserRegisteredEvent(username));
    }
}
```

---

### 🔹 Listener

```java
@Component
public class WelcomeEmailService {

    @EventListener
    public void handleUserRegistered(UserRegisteredEvent event) {
        System.out.println("Sending welcome email to: " + event.getUsername());
    }
}
```

---

### ✅ Output:

```
User registered: malobika
Sending welcome email to: malobika
```

---

## Summary:

> “Spring Events provide a built-in way for beans to communicate in a decoupled, event-driven manner using `ApplicationEventPublisher` and `@EventListener`. It’s great for things like domain events, notifications, and modular design.”
