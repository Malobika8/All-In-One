## Question:

- You're designing a system for an **online food delivery app**. One of the modules is a **DeliveryScheduler** service that decides how to assign a delivery partner to an order, send them a notification, and log the delivery assignment.
- The app currently supports only **bike deliveries**, but soon we may have **drones** and **electric scooters**. Also, sometimes delivery logs are saved to **a database**, and sometimes to a **file system**.
- How would you design this module using SOLID principles?

#### 🧠 Tasks:

1. What classes/interfaces would you create?
2. How would you use **SRP**, **OCP**, **LSP**, **ISP**, and **DIP** in this design?
3. How would you make this design **easy to extend** and **testable**?

---

### Sol:

```
public interface DeliveryService{
    public void assignDelivery();
}
public class BikeDelivery implements DeliveryService{
    @Override
    public void assignDelivery(){
        //deliver through bike...
    }
}
public interface NotificationService{
    public void notify();
}
public class EmailNotification implements NotificationService{
    @Override
    public void notify(){
        //notify through email...
    }
}
public class SmsNotification implements NotificationService{
    @Override
    public void notify(){
        //notify through sms...
    }
}
public interface LogService{
    public void logMessage();
}
public class DatabaseLog implements LogService{
    @Override
    public void logMessage(){
        //log to database...
    }
}
public class FileSystemLog implements LogService{
    @Override
    public void logMessage(){
        //log to file system...
    }
}

public class DeliveryScheduler{
    DeliveryService deliveryService;
    NotificationService notificationService;
    LogService logService;
    
    DeliveryScheduler(DeliveryService deliveryService, NotificationService notificationService, LogService logService){
        this.deliveryService = deliveryService;
        this.notificationService = notificationService;
        this.logService = logService;
    }
    public void deliver(){
        deliveryService.assignDelivery();
        notificationService.notify();
        logService.logMessage();
    }
}
```
---

## ✅ SOLID Principles Applied 

### 🔹 1. **S – Single Responsibility Principle (SRP)**

Each class does **only one job**:

| Class               | Responsibility               |
| ------------------- | ---------------------------- |
| `BikeDelivery`      | Handles how delivery is done |
| `EmailNotification` | Handles email notifications  |
| `DatabaseLog`       | Handles database logging     |

✅ SRP fully respected.

---

### 🔹 2. **O – Open/Closed Principle (OCP)**

* You can **add new delivery modes** (like `DroneDelivery`) or **new log mechanisms** (like `KafkaLog`) **without modifying existing code**.
* You just create a new class that implements the respective interface.

✅ Perfect application of OCP.

---

### 🔹 3. **L – Liskov Substitution Principle (LSP)**

* Designed all interfaces properly, and each implementation **safely substitutes** the abstraction.
* If `DeliveryService delivery = new BikeDelivery();`, it works seamlessly — no broken behavior.

✅ LSP respected.

---

### 🔹 4. **I – Interface Segregation Principle (ISP)**

* Avoided a “fat interface.”
* Each interface (`DeliveryService`, `NotificationService`, `LogService`) is **focused**.

✅ ISP respected.

---

### 🔹 5. **D – Dependency Inversion Principle (DIP)**

* `DeliveryScheduler` depends on **abstractions** (`DeliveryService`, `NotificationService`, `LogService`) instead of concrete classes.
* You **inject dependencies** (e.g., via constructor), so behavior is flexible and testable.

✅ DIP respected.

---
