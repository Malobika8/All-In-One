## **1. `Lock` Interface**

### **Implementation Classes:**
- **`ReentrantLock`**  
  - **Package**: `java.util.concurrent.locks`  
  - A lock that allows a thread to acquire the lock multiple times (reentrancy). It also provides additional features like fairness and interruptibility.

- **`StampedLock`**  
  - **Package**: `java.util.concurrent.locks`  
  - Provides an advanced lock with **optimistic locking** and more fine-grained control over lock acquisition, designed for high-performance scenarios.

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
