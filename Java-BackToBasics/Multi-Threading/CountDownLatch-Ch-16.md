
## 🧠 What is `CountDownLatch`?

`CountDownLatch` is like a **gate** that allows threads to wait until **other threads finish** certain operations.

### 📦 Definition:
```java
public class CountDownLatch
```

It allows one or more threads to **wait until a set of operations being performed in other threads completes**.

---

### 🔧 Constructor:
```java
CountDownLatch latch = new CountDownLatch(int count);
```

- The `count` represents the number of times `countDown()` must be called before threads waiting on the latch can proceed.

---

### ✅ Common Use Case:

> **Wait for multiple threads to finish a task before continuing.**

For example:
- Main thread waits for 3 worker threads to complete.
- Once all workers call `countDown()`, the main thread continues.

---

## 🧩 Example:

```java
import java.util.concurrent.CountDownLatch;

public class LatchExample {

    public static void main(String[] args) throws InterruptedException {
        CountDownLatch latch = new CountDownLatch(3); // 3 tasks to wait for

        Runnable worker = () -> {
            System.out.println(Thread.currentThread().getName() + " is working...");
            try {
                Thread.sleep(1000); // Simulate work
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            }
            latch.countDown(); // Signals task completion
            System.out.println(Thread.currentThread().getName() + " finished.");
        };

        // Start 3 worker threads
        for (int i = 0; i < 3; i++) {
            new Thread(worker).start();
        }

        System.out.println("Main thread is waiting for workers...");
        latch.await(); // Wait until count reaches 0
        System.out.println("All workers finished. Main thread proceeds.");
    }
}
```

---

## 🧰 Key Methods

| Method | Description |
|--------|-------------|
| `await()` | Causes current thread to wait until the count reaches 0 |
| `countDown()` | Decreases the count by 1 |
| `getCount()` | Returns the current count |

---

## ⚠️ Notes

- Once the count reaches 0, it **cannot be reset**.
- If you need something reusable, consider using `CyclicBarrier` or `Semaphore`.

---

## 🔄 Real-world analogy

Imagine a classroom where the teacher (main thread) is waiting for **3 students to finish their test** before collecting papers and leaving. Each student (worker thread) hands in their test (calls `countDown()`). Once all 3 are done, the teacher proceeds (await unblocks).

---

