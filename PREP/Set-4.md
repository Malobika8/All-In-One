# Q30. What is a deadlock? How can it occur in Java?

### **What is a Deadlock?**

A deadlock occurs when **two or more threads are permanently blocked**, each waiting for a resource held by another thread.

### **How Deadlock Occurs (Classic Example)**

* Thread T1 holds **Lock A** and waits for **Lock B**
* Thread T2 holds **Lock B** and waits for **Lock A**
* Neither can proceed → **deadlock**

## Four Necessary Conditions for Deadlock

1. **Mutual Exclusion** – Only one thread can hold a resource
2. **Hold and Wait** – Thread holds one lock while waiting for another
3. **No Preemption** – Locks cannot be forcibly taken
4. **Circular Wait** – Circular dependency between threads

> “Deadlock occurs when threads wait indefinitely for resources held by each other, creating a circular dependency.”

---

# Q31. How can you prevent or avoid deadlock in Java?**

### 1️⃣ **Consistent Lock Ordering** 

* Always acquire locks in the **same order** across all threads

✔️ Example:

```java
synchronized(lockA) {
    synchronized(lockB) {
        // safe
    }
}
```

### 2️⃣ **Avoid Nested Locks**

* Minimize `synchronized` blocks inside other synchronized blocks

### 3️⃣ **Use Try-Lock (`ReentrantLock`)**

* Allows timeout instead of waiting forever

```java
if(lock.tryLock(5, TimeUnit.SECONDS)) {
    try {
        // work
    } finally {
        lock.unlock();
    }
}
```

### 4️⃣ **Use Higher-Level Concurrency APIs**

* `ExecutorService`
* `ConcurrentHashMap`
* `BlockingQueue`

### 5️⃣ **Detect Deadlocks**

* JVM tools:

  * `jconsole`
  * `jstack`

> “Deadlock can be prevented by enforcing consistent lock ordering, avoiding nested locks, and using timeout-based locking.”

---

# Q32. What is the difference between `synchronized` method and `synchronized` block? Which is preferred and why?

### `synchronized` Method

* Synchronizes the **entire method**
* Lock used:

  * Instance method → `this`
  * Static method → `Class` object
* Less flexible
* Can reduce performance due to coarse-grained locking

### `synchronized` Block

* Synchronizes **only the critical section**
* Allows choosing **any object** as lock
* More flexible
* Better performance due to **fine-grained locking**

Example:

```java
synchronized(lock) {
    // critical section
}
```

## Why `synchronized` Block is Preferred

* Locks only what is needed
* Reduces contention
* Improves throughput
* Allows multiple independent locks

> “`synchronized` blocks are preferred over synchronized methods because they provide fine-grained locking and better performance.”

---

# Q33. Is `String` thread-safe in Java? If yes, how? If no, why not?

Yes, `String` is thread-safe because of the following:

* `String` is **immutable**
* Once created, its value **cannot be changed**
* Any modification creates a **new String object**
* Internal character array is:

  * `private`
  * `final`
* No setter methods exist

Because of this:

* Multiple threads can safely share the same `String` instance
* No synchronization is required

## Important Clarification

> `String` is **thread-safe because it is immutable**,
> **not because it uses synchronization**

> “String is thread-safe due to immutability—its state cannot be modified after creation.”

---

# Q34. What is the difference between `HashMap` and `ConcurrentHashMap`?

## Difference: `HashMap` vs `ConcurrentHashMap`

### `HashMap`

* **Not thread-safe**
* Multiple threads can corrupt data
* Can cause:

  * Infinite loops
  * Data inconsistency
* Allows **one null key** and **multiple null values**

### `ConcurrentHashMap`

* **Thread-safe**
* Designed for **high concurrency**
* Does **not lock the entire map**
* Multiple threads can read/write safely
* **Does not allow null keys or null values**

## Important Note ⚠️ (Java 8+)

* **Before Java 8** → Segment-based locking
* **Java 8 onwards** →

  * Uses **bucket-level locking**
  * Uses **CAS (Compare-And-Swap)**
  * Uses `synchronized` on nodes when needed

> “ConcurrentHashMap is thread-safe and provides high concurrency by locking only small portions of the map instead of the whole map.”

---

# Q35. Difference between `ArrayList` and `LinkedList`? When would you use each?



