### ✅ The Problem:

In monolithic apps, we have a **single database**, so we can use:

* ACID transactions (atomicity, consistency, isolation, durability)
* Example: Use a single `BEGIN; ... COMMIT;` to wrap changes across multiple tables

---

### ❌ But in microservices:

Each service has **its own database**, so there's **no distributed transaction manager** across services like:

* OrderService (uses `order_db`)
* PaymentService (uses `payment_db`)

You can’t do:

```sql
BEGIN;
INSERT INTO orders ... ;
INSERT INTO payments ... ;
COMMIT;
```

If one call fails, your system may become **inconsistent**.

---

### ✅ Solution: **Saga Pattern**

The **Saga Pattern** solves this by breaking the distributed transaction into a **sequence of local transactions** that are coordinated via:

* **Events**
* Orchestration logic
* **Compensating actions** (like rollbacks)

---

### ✅ Two Ways to Implement Saga:

#### 1. **Choreography (Event-based, Decentralized)**

Each service performs its transaction and **publishes an event**.
The next service **listens to the event** and does its work.

✅ No central coordinator.

🧠 Example:

1. `OrderService` creates order → emits `OrderCreated`
2. `PaymentService` listens to `OrderCreated`, processes payment → emits `PaymentSuccess`
3. `ShippingService` listens to `PaymentSuccess`, ships item

If something fails, services emit **compensating events** to undo prior actions.

---

#### 2. **Orchestration (Central Coordinator)**

A **central orchestrator** (like a SagaService or workflow engine) tells each service what to do step by step.

✅ More control, centralized logic.

🧠 Example:

* Orchestrator calls `OrderService.createOrder()`
* Then calls `PaymentService.pay()`
* Then calls `ShippingService.ship()`

If `PaymentService` fails, it calls `OrderService.cancelOrder()` as a **compensating transaction**.

---

### ✅ Real-World Analogy:

Imagine you book:

* A flight
* A hotel
* A rental car

If the hotel booking fails, you want to **cancel the flight and car** → those are **compensating actions** in a **Saga**.

---

### ✅ Key Points:

* Saga ensures **eventual consistency**, not strict ACID.
* Saga uses **local transactions** and **compensating transactions**.
* Two models: **choreography (event-based)** and **orchestration (central coordinator)**.
* Tools: you can implement with **Spring Boot + Kafka** or use frameworks like **Axon, Camunda**, or **Temporal**.

---

\
