## 🔹 Fault Tolerance

**Definition:**
Fault tolerance is the **ability of a system to continue operating correctly even when one or more components fail**.

**Key Points:**

* The system **absorbs faults without affecting overall behavior**.
* It’s usually achieved through **redundancy**, **failover**, **replication**, etc.
* Example: If one server in a cluster fails, traffic is rerouted to another healthy server automatically.

**Goal:** Keep the system working **without interruption** during faults.

---

## 🔹 Resilience

**Definition:**
Resilience is the **ability of a system to recover quickly from failures and continue to function**, often in a **degraded** state.

**Key Points:**

* A resilient system may **not prevent failure**, but it **recovers gracefully**.
* It includes **fault detection**, **self-healing**, and **adaptive mechanisms**.
* Example: A system using a circuit breaker to stop calling a failing downstream service and return a default response.

**Goal:** Ensure the system **recovers and keeps delivering value**, even if reduced.

---

### 🔁 Fault Tolerance vs Resilience — Summary Table

| Aspect           | Fault Tolerance                       | Resilience                                   |
| ---------------- | ------------------------------------- | -------------------------------------------- |
| Focus            | Continue operating **during** a fault | **Recover** and adapt after fault            |
| Failure Handling | Hide or mask the failure              | Detect and recover from failure              |
| Techniques       | Replication, redundancy, failover     | Circuit breakers, retries, backoff, fallback |
| Example          | Load balancer rerouting traffic       | Netflix Hystrix cutting off failing service  |
| Goal             | **No disruption**                     | **Graceful degradation and recovery**        |

---

### ✅ Are They the Same?

> **No**, but they **work together**.
> You can think of it this way:

> 🔸 Fault tolerance is a **subset** of resilience.
> 🔸 A **resilient system may use fault-tolerant components**, but it also focuses on **recovery and adaptability**.

---

Let’s understand **Fault Tolerance vs Resilience** with:

## 🔧 Real-World Analogy

### 🎛️ Fault Tolerance — "Backup Generator"

Imagine a hospital that **can’t afford power outages**.

* So, they install a **backup generator**.
* If the main power fails, the generator kicks in instantly.
* **No one notices the failure.**

🟢 This is **fault tolerance** — the failure happens, but the system keeps working **without disruption**.

---

### 💪 Resilience — "Emergency Plan"

Now suppose:

* The generator also fails 😱
* But the hospital has **manual emergency protocols**: battery-powered lights, oxygen cylinders, offline records, etc.
* The hospital **still functions**, but at a **reduced capacity**, until power is restored.

🟢 This is **resilience** — the system **adapts and survives** even with multiple failures.

---

## 💻 Spring Boot Example

### Scenario: Your app calls an external payment service.

---

### 🟢 Fault Tolerance:

You use **Spring Cloud LoadBalancer** + **retry** + **failover URLs**.

```java
@Retryable(value = RemoteServiceException.class, maxAttempts = 3)
public PaymentResponse callPaymentService() {
    // Try primary URL first, fallback to backup
}
```

* If one instance fails, it retries.
* Or switches to backup.
* **User doesn't notice.**

---

### 🟢 Resilience:

You add **resilience features** using [Resilience4j](https://resilience4j.readme.io/) (a fault-tolerance library):

```java
@CircuitBreaker(name = "paymentService", fallbackMethod = "fallbackPayment")
public PaymentResponse callPaymentService() {
    // External call
}

public PaymentResponse fallbackPayment(Exception e) {
    return new PaymentResponse("Service temporarily unavailable. Try later.");
}
```

* If the payment service fails multiple times, the **circuit opens**.
* Your system **stops trying** the failing service and **returns a default response** instead of breaking.

✅ The system **recovers gracefully**, maybe with **degraded service**, but **doesn't crash**.

---

## 📌 Conclusion (One-liner):

* **Fault Tolerance** = “I’ll keep running even if something breaks.”
* **Resilience** = “Even if I break, I’ll bounce back.”

---
