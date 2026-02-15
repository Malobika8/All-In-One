## **1. `Lock` Interface**

### **Implementation Classes:**
- **`ReentrantLock`**  
  - **Package**: `java.util.concurrent.locks`  
  - A lock that allows a thread to acquire the lock multiple times (reentrancy). It also provides additional features like fairness and interruptibility.

- **`StampedLock`**  
  - **Package**: `java.util.concurrent.locks`  
  - Provides an advanced lock with **optimistic locking** and more fine-grained control over lock acquisition, designed for high-performance scenarios.
 
StampedLock was introduced in Java 8. It is designed for high-performance read-heavy systems.

Key idea: It introduces Optimistic Locking.

### Features of StampedLock

It provides three modes:

1️⃣ Write Lock
2️⃣ Read Lock
3️⃣ Optimistic Read

#### What is Optimistic Read?

This is the powerful part. Instead of blocking readers: It allows a thread to read without locking. It returns a stamp (version number). After reading, you validate the stamp. If no write happened → data is valid. If write happened → retry with proper read lock.

#### Why is this powerful?

In read-heavy systems: Most of the time, no write happens. So optimistic reads succeed. No blocking. No context switching. Very high throughput.

#### Example Use Case

Market data system: 1000 threads reading stock price 1 thread updating price occasionally

#### ReentrantReadWriteLock:
- Readers still acquire read lock.

#### StampedLock:
- Readers use optimistic read.
- Much faster.


#### StampedLock is:

- Not reentrant
- Not condition-based
- Harder to use correctly
- Not always better
- You use it only in performance-critical read-heavy systems.

### When would you NOT use StampedLock?

- When reentrancy is required
- When condition variables are needed
- When simplicity is more important than raw performance

---

## **2. `ReadWriteLock` Interface**

### **Implementation Classes:**
- **`ReentrantReadWriteLock`**  
  - **Package**: `java.util.concurrent.locks`  
  - A read-write lock that allows multiple threads to read a resource concurrently, but only one thread to write to it at a time. Supports reentrancy.

---

## **3. `Condition` Interface**

### **Implementation Classes:**
- **`Object.wait()`**, **`Object.notify()`**, and **`Object.notifyAll()`**  
  - While not classes themselves, these are **methods of `Object`** used to implement basic waiting and signaling mechanisms.
  - Used in conjunction with any **`Lock`** (such as `ReentrantLock`) to achieve the same functionality as a `Condition` object.

---

So, to summarize:

1. **`Lock`** → `ReentrantLock`, `StampedLock`
2. **`ReadWriteLock`** → `ReentrantReadWriteLock`
3. **`Condition`** → Implemented by methods in `Object` (no direct classes for `Condition`).
