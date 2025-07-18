# What is the difference between a process and a thread?

### Sol:

#### 🔹**Process:**

* A **process** is an independent unit of execution that has **its own memory space**.
* It represents a running instance of a program (like Word, Excel, or Chrome).
* Processes do **not share memory** with each other by default.

#### 🔹**Thread:**

* A **thread** is a **smaller unit of execution within a process**.
* All threads of the same process **share memory and resources** (like heap, open files).
* Threads are used to perform **tasks concurrently** within the same application — e.g., spell checking and auto-saving in Word.

#### 🔹Key Differences:

| Feature       | Process                       | Thread                             |
| ------------- | ----------------------------- | ---------------------------------- |
| Memory        | Separate memory               | Shared memory within process       |
| Overhead      | High (context switching, etc) | Low                                |
| Communication | Inter-process communication   | Shared memory (simpler, faster)    |
| Crash impact  | One process crash is isolated | Thread crash may affect entire app |

---

# **What are the different ways to create threads in Java? Explain when you'd use each.**

### Sol:

#### 1. **Extending the `Thread` class**

```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread running...");
    }
}
new MyThread().start();
```

* **Use when**: You don’t need to extend any other class (since Java doesn’t support multiple inheritance).
* **Limitation**: Less flexible, as your class can't extend anything else.

#### 2. **Implementing the `Runnable` interface**

```java
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Runnable thread running...");
    }
}
Thread t = new Thread(new MyRunnable());
t.start();
```

* **Use when**: You want to extend another class or keep your task decoupled from the Thread object.
* **Preferred** for most use cases due to better separation of concerns.

#### 3. **Using the `Callable` interface with `ExecutorService`**

```java
Callable<String> task = () -> {
    return "Callable result";
};

ExecutorService service = Executors.newSingleThreadExecutor();
Future<String> future = service.submit(task);
String result = future.get();  // blocks until done
service.shutdown();
```

* **Callable** can return a value and throw checked exceptions.
* **Use when**: You need a result from the thread or exception handling.

---

# What are the different states of a thread in Java, and what triggers each transition between those states?

### Sol:

1. #### **NEW**

   * A thread is created but **not started** yet.
   * Example: `Thread t = new Thread();`

2. #### **RUNNABLE**

   * The thread has been started using `start()`.
   * It's ready to run and **waiting for CPU scheduling**.
   * Might be actively running or waiting in the thread scheduler's queue.

3. #### **BLOCKED**

   * Thread is waiting to **acquire a monitor lock** (e.g., `synchronized` block).
   * Only applies when **another thread is holding the lock**.

4. #### **WAITING**

   * Thread is **waiting indefinitely** for another thread to perform a particular action:

     * `wait()`, `join()`, or `LockSupport.park()`.
   * It will only resume if explicitly **notified**.

5. #### **TIMED\_WAITING**

   * Similar to `WAITING`, but with a **timeout**.
   * Example methods: `sleep(ms)`, `join(ms)`, `wait(ms)`, `Thread.sleep(1000)`

6. #### **TERMINATED (or DEAD)**

   * Thread completes execution or terminates due to an exception.

#### Transitions Summary

| From                                      | To                                                   | Trigger |
| ----------------------------------------- | ---------------------------------------------------- | ------- |
| NEW → RUNNABLE                            | `start()`                                            |         |
| RUNNABLE → BLOCKED                        | Tries to enter `synchronized` block but lock is held |         |
| RUNNABLE → WAITING                        | Calls `wait()`, `join()`, etc.                       |         |
| RUNNABLE → TIMED\_WAITING                 | Calls `sleep(1000)`, `wait(1000)`, etc.              |         |
| BLOCKED/WAITING/TIMED\_WAITING → RUNNABLE | Lock released / notified / timeout over              |         |
| RUNNABLE → TERMINATED                     | `run()` method ends or exception occurs              |         |

---

# Write a program where:

* Two threads print numbers from 1 to 10.
* One thread prints **odd numbers**, another prints **even numbers**.
* Output should alternate correctly: 1, 2, 3, 4, …

Use `synchronized`, `wait()`, and `notify()`.

### Sol:

```
public class Main {
    private static final Object lock = new Object();
    private static int i = 1;
    private static final int MAX = 10;

    public static void main(String[] args) {
        Runnable evenRunnable = () -> {
            while (i <= MAX) {
                synchronized (lock) {
                    if (i % 2 == 0) {
                        System.out.println("Even: " + i);
                        i++;
                        lock.notify();
                    } else {
                        try {
                            lock.wait();
                        } catch (InterruptedException ex) {
                            System.out.println(ex);
                        }
                    }
                }
            }
        };

        Runnable oddRunnable = () -> {
            while (i <= MAX) {
                synchronized (lock) {
                    if (i % 2 != 0) {
                        System.out.println("Odd: " + i);
                        i++;
                        lock.notify();
                    } else {
                        try {
                            lock.wait();
                        } catch (InterruptedException ex) {
                            System.out.println(ex);
                        }
                    }
                }
            }
        };

        Thread thread1 = new Thread(evenRunnable);
        Thread thread2 = new Thread(oddRunnable);

        thread1.start();
        thread2.start();
    }
}
```

---

# What is the difference between wait(), sleep(), and join() in Java multithreading?

### Sol:

| Method    | Defined In         | Requires Lock | Releases Lock | Wakes Automatically?                     | Use Case                                                                          |
| --------- | ------------------ | ------------- | ------------- | ---------------------------------------- | --------------------------------------------------------------------------------- |
| `wait()`  | `java.lang.Object` | ✅ Yes         | ✅ Yes         | ❌ No (needs `notify()` or `notifyAll()`) | To **pause** a thread until another thread notifies it (usually for coordination) |
| `sleep()` | `java.lang.Thread` | ❌ No          | ❌ No          | ✅ Yes (after timeout)                    | To **pause execution** for a fixed time without releasing lock                    |
| `join()`  | `java.lang.Thread` | ❌ No          | ❌ No          | ✅ Yes (when other thread finishes)       | To **wait for a thread to finish** before continuing                              |

#### 1. **wait()**

* Belongs to the `Object` class (because every object can be a lock).
* Must be called **inside a synchronized block**.
* Releases the lock and puts the thread in **WAITING** state.
* Another thread must call `notify()`/`notifyAll()` on the same lock object to wake it up.

```java
synchronized(lock) {
    lock.wait(); // thread waits and releases the lock
}
```

#### 2. **sleep()**

* Belongs to `Thread` class.
* Puts the thread into **TIMED\_WAITING** state for the given time.
* **Does not release any locks**.
* Used for delaying execution without coordination.

```java
Thread.sleep(1000); // sleep for 1 second
```

#### 3. **join()**

* Called on a thread to **wait until it finishes execution**.
* Commonly used in `main()` to wait for child threads.

```java
Thread t = new Thread(() -> {
    // do work
});
t.start();
t.join(); // main thread waits for t to finish
```

---

# What is the difference between `synchronized` block and `synchronized` method in Java? And which one is better to use in practice?

### Sol:

#### `synchronized` Method

* Locks the **entire method**.
* If it's an instance method, the lock is on the **current object (`this`)**.
* If it's a static method, the lock is on the **class object (`ClassName.class`)**.

```java
public synchronized void update() {
    // only one thread can execute this entire method at a time
}
```

#### `synchronized` Block

* Locks **only a portion** of code inside a method.
* You can specify **any object** as the lock.
* Gives you **fine-grained control**, reducing the time the lock is held → better performance.

```java
public void update() {
    // non-critical code

    synchronized(lockObject) {
        // critical section
    }

    // non-critical code
}
```

✅ **`synchronized` block is preferred** in most real-world scenarios because:

* It avoids locking the entire method unnecessarily.
* You can synchronize on **different objects** instead of `this` (allowing parallelism).
* It leads to **better concurrency and performance**.

---

#Quiz:

> You have a method where only 2 lines access a shared resource.
> Would you mark the whole method `synchronized`, or just those 2 lines?
> And why?

### Sol:

I would only put those 2 lines in a synchronized block, not the entire method.
This minimizes the lock duration, allowing other threads to execute the non-critical parts of the method without waiting unnecessarily.
It improves performance and thread throughput, especially in high-concurrency environments.

---

# Write a Java class Counter that:
- Has a shared count variable.
- Two threads increment count 1000 times each.
- Use synchronized to ensure thread safety.
- Finally, print the correct final value of count (should be 2000).

## Sol:

```
public class Main {
    private static int count = 0;
    private static final Object lock = new Object();

    public static void main(String[] args) throws InterruptedException {
        Runnable incrementTask = () -> {
            for (int i = 0; i < 1000; i++) {
                synchronized (lock) {
                    count++;
                }
            }
        };

        Thread thread1 = new Thread(incrementTask);
        Thread thread2 = new Thread(incrementTask);

        thread1.start();
        thread2.start();

        thread1.join();
        thread2.join();

        System.out.println("Final count: " + count); // Should be 2000
    }
}
```

---

# What is a race condition in Java multithreading? How does synchronized help prevent it?

## Sol:

✅ Excellent answer — very clear, and you captured both the **problem** and the **solution** perfectly!

> A **race condition** occurs when **multiple threads** access and modify a **shared resource** at the same time, and the final outcome depends on the timing of their execution.
> This leads to **unpredictable behavior** and **inconsistent or corrupt data**.

#### Example:

If two threads increment the same variable `count++` at the same time, the result might be wrong (e.g., still 1 instead of 2) because the increment is **not atomic**.

> The `synchronized` keyword ensures that **only one thread at a time** can execute the **critical section** of code (i.e., the part that accesses or modifies shared data).
> It does this by acquiring a **monitor lock** on an object. Other threads are **blocked** until the lock is released.

#### This guarantees:

* **Mutual exclusion**
* **Thread-safe access**
* **Consistent results**

---





