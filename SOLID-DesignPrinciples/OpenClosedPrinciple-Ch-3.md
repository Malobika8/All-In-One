## Open/Closed Principle (OCP)

### ✅ **Definition:**

> Software entities (classes, modules, functions) should be **open for extension**, but **closed for modification**.

---

### 🔍 What does that mean?

You should be able to **add new behavior** to a class **without changing its existing code**.

This encourages:

* Extending via **inheritance** or **composition**
* Using **polymorphism** (e.g., interface-based design)
* Avoiding if-else or switch statements for behavior decisions

---

## ❌ Bad Example (Violates OCP):

```java
public class NotificationService {
    public void send(String type, String message) {
        if ("email".equals(type)) {
            System.out.println("Sending email: " + message);
        } else if ("sms".equals(type)) {
            System.out.println("Sending SMS: " + message);
        } else if ("push".equals(type)) {
            System.out.println("Sending Push: " + message);
        }
    }
}
```

🔴 **Problem**:

* Adding a new type (like WhatsApp) requires **modifying existing code**.
* Risky and error-prone.

---

## ✅ Good Example (Follows OCP):

### Step 1: Create interface

```java
public interface Notifier {
    void send(String message);
}
```

### Step 2: Implement different behaviors

```java
public class EmailNotifier implements Notifier {
    public void send(String message) {
        System.out.println("Sending email: " + message);
    }
}

public class SMSNotifier implements Notifier {
    public void send(String message) {
        System.out.println("Sending SMS: " + message);
    }
}
```

### Step 3: Use them in a flexible way

```java
public class NotificationService {
    private final Notifier notifier;

    public NotificationService(Notifier notifier) {
        this.notifier = notifier;
    }

    public void notify(String message) {
        notifier.send(message);
    }
}
```

### ✅ Now to support WhatsApp:

* You **don’t change** `NotificationService`
* You **just create a new class**:

```java
public class WhatsAppNotifier implements Notifier {
    public void send(String message) {
        System.out.println("Sending WhatsApp: " + message);
    }
}
```

---

## 🧠 Why OCP Matters in Real Life

* Protects working code from unintended bugs
* Encourages **plug-and-play** architecture
* Essential for maintaining large codebases (especially in microservices)

---

## 💬 Questions:

🗣️ **Q:** What does Open/Closed Principle mean?

✅ *A class should be open for extension but closed for modification. That means I should be able to extend its behavior without editing its code.*

🗣️ **Q:** How do you achieve this in Java?

✅ *By using interfaces, abstract classes, and dependency injection to inject new behavior.*

🗣️ **Q:** Can you give a real-world Spring example?

✅ *Yes! The Spring `ApplicationEventPublisher` allows me to define events. I can add new listeners without modifying the event publisher logic — that’s OCP in action.*

🗣️ **Q:** You are asked to build a simple **PaymentProcessor**. The current code supports only **Credit Card payments**.

Now your team wants to support **UPI** and **PayPal** as well. Below is the current code:

```java
public class PaymentProcessor {
    public void pay(String method, double amount) {
        if (method.equals("creditcard")) {
            System.out.println("Paid ₹" + amount + " via Credit Card.");
        }
    }
}
```

#### Your Tasks:

1. ✅ Does this violate OCP?
2. ✅ Refactor this code to follow Open/Closed Principle.

   * Add support for **UPI** and **PayPal**
   * Make sure you can add more payment methods in future **without modifying** the `PaymentProcessor`

#### Sol:

```java
public interface Payment {
    void pay(double amount);
}
```
```java
public class CreditCardPayment implements Payment {
    public void pay(double amount) {
        System.out.println("Paid ₹" + amount + " via Credit Card.");
    }
}

public class UpiPayment implements Payment {
    public void pay(double amount) {
        System.out.println("Paid ₹" + amount + " via UPI.");
    }
}

public class PaypalPayment implements Payment {
    public void pay(double amount) {
        System.out.println("Paid ₹" + amount + " via PayPal.");
    }
}
```
```java
public class PaymentProcessor {
    private final Payment payment;

    public PaymentProcessor(Payment payment) {
        this.payment = payment;
    }

    public void process(double amount) {
        payment.pay(amount);
    }
}
```
```java
public class Main {
    public static void main(String[] args) {
        Payment payment = new UpiPayment(); // You can switch to PaypalPayment etc.
        PaymentProcessor processor = new PaymentProcessor(payment);
        processor.process(999.99);
    }
}
```

#### Now if you want to support CryptoPayments:

> 🔄 Just add a `CryptoPayment` class — no need to touch `PaymentProcessor`.

---

## ✅ Summary:

| ✅ Principle                               | ✅ Response |
| ----------------------------------------- | --------------- |
| Avoid modifying working code              | ✔️ Yes          |
| Extend using interface/implementations    | ✔️ Yes          |
| Dependency injected instead of hard-coded | ✔️ Yes          |
| Easy to add new behavior                  | ✔️ Yes          |

---





