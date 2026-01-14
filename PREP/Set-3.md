# Q21. What does intern() do in Java Strings? When would you use it?

> `intern()` returns a **canonical representation** of the String from the **String Constant Pool.

### How it actually works

```java
String s1 = new String("java");
String s2 = s1.intern();
```

Steps:

1. JVM checks if `"java"` exists in the String Constant Pool
2. If it exists → returns reference to the pooled String
3. If it does not exist → adds it to the pool and returns it

👉 `s2` points to the pooled string
👉 `s1` still points to the heap object

* `new String()` **always creates a new heap object**
* `intern()` only affects the **reference you get back**

## When would you use `intern()`?

* To reduce memory usage when:

  * Many duplicate Strings exist
* When you want:

  * Reference equality (`==`) for identical strings

⚠️ Use carefully — excessive interning can increase GC pressure.
`intern()` returns the pooled String reference from the String Constant Pool. It does not prevent heap object creation, but helps reuse canonical Strings.

---

# Q22. Is `StringBuilder` thread-safe? Is `StringBuffer` thread-safe? Why?

* **`StringBuilder` is NOT thread-safe**
  * Methods are **not synchronized**
  * Faster
  * Preferred in **single-threaded** or local usage

* **`StringBuffer` IS thread-safe**
  * Methods are **synchronized**
  * Safer in multi-threaded environments
  * Slightly **slower due to synchronization overhead**

* Both are **mutable**
  * They modify the same object instead of creating new ones (unlike `String`)

> Even though `StringBuffer` is thread-safe, in modern Java we usually prefer `StringBuilder` and handle synchronization externally if needed.

## Quick Comparison Table

| Feature     | String      | StringBuilder | StringBuffer   |
| ----------- | ----------- | ------------- | -------------- |
| Mutability  | ❌ Immutable | ✅ Mutable     | ✅ Mutable      |
| Thread-safe | ✅ Yes       | ❌ No          | ✅ Yes          |
| Performance | Slow        | Fast          | Slower than SB |

---

# Q23. Difference between `checked` and `unchecked` exceptions? Give examples and when to use each.

### Checked Exceptions

* Checked at **compile time**
* Compiler **forces handling**

  * `try–catch` **or**
  * `throws` declaration
* Represent **recoverable conditions**

**Examples:**

* `SQLException`
* `IOException`
* `FileNotFoundException`

### Unchecked Exceptions

* Checked at **runtime**
* Compiler does **not force handling**
* Extend `RuntimeException`
* Usually indicate **programming errors**

**Examples:**

* `NullPointerException`
* `ArrayIndexOutOfBoundsException`
* `ArithmeticException`

## When to Use Which?

* Use **checked exceptions** when:

  * Caller can reasonably recover
  * External resources are involved (DB, file, network)

* Use **unchecked exceptions** when:

  * Error indicates a bug
  * Recovery is not meaningful

> Checked exceptions represent recoverable conditions and must be handled at compile time, while unchecked exceptions represent programming errors and are checked at runtime.

---

# Q24. Can we override a method and throw a broader exception than the parent method? Explain with rules.

### **In method overriding:**

#### 1️⃣ For **checked exceptions**

* **You CANNOT throw a broader checked exception**
* You can:

  * Throw the **same exception**
  * Throw a **subclass (narrower exception)**
  * Throw **no exception**

#### 2️⃣ For **unchecked exceptions**

* You CAN throw **any unchecked exception**
* No restriction

## Example (Checked Exception )

```java
class Parent {
    void read() throws IOException {}
}

class Child extends Parent {
    // Compilation error
    void read() throws Exception {}
}
```

Why?

* `Exception` is broader than `IOException`

## Correct Overriding

```java
class Child extends Parent {
    void read() throws FileNotFoundException {}
}
```

✔ Allowed — narrower exception

## Unchecked Exception Case

```java
class Parent {
    void process() {}
}

class Child extends Parent {
    void process() throws RuntimeException {} // allowed
}
```

> “While overriding, a method cannot throw a broader checked exception than the parent method, but it can throw narrower checked exceptions or any unchecked exception.”

> “What if parent method throws no exception?”

Answer:

* Child **cannot** throw checked exceptions
* Child **can** throw unchecked exceptions

---

# Q25. What is the difference between `throw` and `throws`?

✅ **Correct. Concise. Interview-acceptable.**
I’ll just tighten the wording slightly and add one tiny clarification that interviewers like.

---

## Polished Interview Answer 🏆

### `throw`

* Used to **explicitly throw an exception**
* Used **inside a method or block**
* Throws **one exception object at a time**

Example:

```java
throw new IllegalArgumentException("Invalid input");
```

---

### `throws`

* Used in **method declaration**
* Indicates that the method **may propagate an exception**
* Can declare **multiple exceptions**

Example:

```java
void readFile() throws IOException, SQLException {
}
```

---

## Key Difference (One-Line)

> "`throw` is used to actually throw an exception, while `throws` is used to declare that a method might throw exceptions."

* `throws` applies mainly to **checked exceptions**
* Unchecked exceptions don’t need to be declared


---

# Q26. What happens if an exception is thrown in the `finally` block? Which exception will be propagated?

### Can we throw an exception from `finally`?

**Yes, we can.**

### What happens if an exception is thrown in `finally`?

> **The exception thrown in the `finally` block will override any exception thrown in the `try` or `catch` block.**

## Example

```java
try {
    throw new RuntimeException("Exception from try");
} finally {
    throw new RuntimeException("Exception from finally");
}
```

### Output:

```
RuntimeException: Exception from finally
```

The original exception is **lost** (suppressed).

> “If both `try` and `finally` throw exceptions, the exception from the `finally` block is propagated and the original exception is lost.”

## Modern Java Note

With **try-with-resources**, Java preserves suppressed exceptions:

```java
Throwable.getSuppressed()
```

---

# Q27. What is the difference between `process` and `thread`?

### **Process**

* A **process** is an **independent program in execution**
* Has its **own memory space (heap, stack, code, data)**
* Processes are **isolated** from each other
* Communication between processes is **expensive** (IPC)

✅ Example:

* Chrome browser
* MS Word
* IntelliJ IDE
  Each runs as a **separate process**

### **Thread**

* A **thread is a lightweight unit of execution inside a process**
* Multiple threads **share the same memory** of the process
* Threads are used for **parallelism and responsiveness**
* Communication between threads is **cheap** (shared memory)

✅ Example:

* In MS Word:

  * UI thread
  * Spell-check thread
  * Auto-save thread

> ✔️ These are **threads**, not processes.

## Key Differences (Short & Sharp)

| Process             | Thread               |
| ------------------- | -------------------- |
| Heavyweight         | Lightweight          |
| Own memory          | Shared memory        |
| Slow context switch | Fast context switch  |
| Independent         | Dependent on process |

> “A process is an independent program with its own memory, whereas a thread is a lightweight execution unit within a process sharing the same memory.”

---

# Q28. How do you create a thread in Java? Which approach is better and why?

There are **two ways to create a thread in Java**:

1. **By extending `Thread` class** and overriding the `run()` method
2. **By implementing `Runnable` interface** and passing it to a `Thread` object

### Why `Runnable` is preferred:

* Java does **not support multiple inheritance of classes**
* A class implementing `Runnable` can still extend another class
* **Separation of concern**:

  * `Runnable` → task
  * `Thread` → execution
* More flexible and **better design**

> “Implementing `Runnable` is preferred over extending `Thread` because it supports better design and allows inheritance from other classes.”


> *“Does extending Thread also use Runnable internally?”*

✔️ Yes — `Thread` itself **implements `Runnable`**.

---

# Q28. What is the difference between `start()` and `run()` method in Java threads?

### `run()` method

* Contains the **actual task / business logic**
* Comes from the `Runnable` interface
* **Calling `run()` directly does NOT create a new thread**
* It executes like a **normal method call** on the current thread

### `start()` method

* Belongs to the `Thread` class
* **Creates a new thread**
* Internally calls `run()` **in a new call stack**
* Puts the thread in **runnable state**
* Thread scheduling is decided by the **JVM / OS scheduler**
* Calling `start()` twice on the same thread causes:

  ```
  IllegalThreadStateException
  ```

> ❌ “puts the task in queue”

More accurate phrasing:

> ✔️ “Registers the thread with the scheduler and moves it to runnable state”

> “Calling `run()` executes the code like a normal method, whereas `start()` creates a new thread and executes `run()` asynchronously.”

## Tiny Code Example

```java
Thread t = new Thread(() -> System.out.println(Thread.currentThread().getName()));

t.run();   // main thread
t.start(); // new thread
```

---

# Q29. What are the different states of a thread in Java? Explain briefly.

## Thread States in Java (As per `Thread.State` enum)

Java has **6 thread states**.

### 1️⃣ **NEW**

* Thread object created
* `start()` not called yet

### 2️⃣ **RUNNABLE**

* Thread is **ready or running**
* JVM may be executing it or waiting for CPU time

⚠️ Java does **not** distinguish between “ready” and “running”

### 3️⃣ **BLOCKED**

* Thread is **waiting to acquire a monitor lock**
* Happens with `synchronized` blocks/methods

Example:

```java
synchronized(lock) {
    // another thread already holds lock
}
```

### 4️⃣ **WAITING**

* Thread waits **indefinitely** for another thread’s action
* Caused by:

  * `wait()`
  * `join()`
  * `park()`

### 5️⃣ **TIMED_WAITING**

* Thread waits for a **fixed amount of time**
* Caused by:

  * `sleep(time)`
  * `wait(time)`
  * `join(time)`

### 6️⃣ **TERMINATED**

* Thread has completed execution
* `run()` method finished

> “Java defines six thread states: NEW, RUNNABLE, BLOCKED, WAITING, TIMED_WAITING, and TERMINATED.”

---

# Q30. What is the difference between `wait()` and `sleep()`?

### `wait()`

* Comes from **`Object` class**
* Must be called **inside a synchronized block/method**
* Causes the thread to:

  * **Release the monitor lock**
  * Enter **WAITING / TIMED_WAITING** state
* Thread resumes **only after**:

  * `notify()` / `notifyAll()` is called
  * (and then it must re-acquire the lock)

> ❌ “wait till other threads finish some task”
> ✔️ “waits until another thread explicitly notifies it”

### `sleep()`

* Comes from **`Thread` class**
* Does **not release the lock**
* Puts the thread in **TIMED_WAITING** state
* Wakes up automatically after the given time
* No dependency on other threads

## Key Differences

| Aspect                | wait()                     | sleep()         |
| --------------------- | -------------------------- | --------------- |
| Class                 | Object                     | Thread          |
| Lock released         | ✅ Yes                      | ❌ No            |
| Needs synchronization | ✅ Yes                      | ❌ No            |
| Wake-up               | notify / notifyAll         | Time-based      |
| Purpose               | Inter-thread communication | Pause execution |

> “`wait()` releases the lock and waits for notification, whereas `sleep()` pauses execution without releasing the lock.”











