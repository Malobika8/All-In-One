Let's see a **multi-threaded example** using `ReadWriteLock` in action, so we can **see how multiple readers can access simultaneously** while **writers get exclusive access**.

---

## ✅ Example: Multiple Readers, One Writer

```java
import java.util.concurrent.locks.*;

class SharedData {
    private int value = 0;

    // Create a ReadWriteLock
    private final ReadWriteLock rwLock = new ReentrantReadWriteLock();

    // Get read and write locks
    private final Lock readLock = rwLock.readLock();
    private final Lock writeLock = rwLock.writeLock();

    // Method for reading the value
    public void readData(String threadName) {
        readLock.lock();
        try {
            System.out.println(threadName + " is READING value: " + value);
            Thread.sleep(1000); // Simulate read time
            System.out.println(threadName + " finished READING");
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        } finally {
            readLock.unlock();
        }
    }

    // Method for writing a new value
    public void writeData(String threadName, int newValue) {
        writeLock.lock();
        try {
            System.out.println(threadName + " is WRITING value: " + newValue);
            Thread.sleep(2000); // Simulate write time
            this.value = newValue;
            System.out.println(threadName + " finished WRITING");
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        } finally {
            writeLock.unlock();
        }
    }
}

public class ReadWriteLockDemo {
    public static void main(String[] args) {
        SharedData data = new SharedData();

        // Create reader threads
        Runnable readTask = () -> {
            String name = Thread.currentThread().getName();
            data.readData(name);
        };

        // Create writer threads
        Runnable writeTask = () -> {
            String name = Thread.currentThread().getName();
            int newValue = (int) (Math.random() * 100);
            data.writeData(name, newValue);
        };

        // Start threads
        Thread t1 = new Thread(readTask, "Reader-1");
        Thread t2 = new Thread(readTask, "Reader-2");
        Thread t3 = new Thread(writeTask, "Writer-1");
        Thread t4 = new Thread(readTask, "Reader-3");
        Thread t5 = new Thread(writeTask, "Writer-2");

        t1.start();
        t2.start();
        t3.start();
        t4.start();
        t5.start();
    }
}
```

---

## 🔍 What we’ll see

- `Reader-1` and `Reader-2` can read **simultaneously**.
- When `Writer-1` starts, it **blocks all other threads**.
- `Reader-3` and `Writer-2` have to **wait** until `Writer-1` is done.

---

This is a **classic read-write lock scenario**:
- Maximize read concurrency ✅
- Maintain data consistency during writes ✅

---

### ✅ **Read Lock Rules (`readLock.lock()`)**:

- ✅ Multiple threads can **hold the read lock simultaneously**.
- ❌ **No thread can acquire the write lock** if **any** read lock is held.
- ✅ Reads can continue **as long as no write is pending or active**.

---

### ✍️ **Write Lock Rules (`writeLock.lock()`)**:

- ❌ No other thread can **read or write** while the write lock is held.
- ✅ Only **one thread** can hold the write lock at a time.
- ✅ It blocks **new readers** too — ensuring complete exclusive access.

---

### 🧠 Mental Model:

| Current Lock State | Can New Readers Enter? | Can Writer Enter? |
|--------------------|------------------------|--------------------|
| No Lock Held       | ✅ Yes                 | ✅ Yes             |
| One or More Readers| ✅ Yes                 | ❌ No              |
| Writer Holding Lock| ❌ No                  | ❌ No              |

---

### 🔄 In Short:
- **Multiple Reads** → ✅ Allowed at the same time.
- **Writes** → 🔐 Exclusive, blocks everyone.
- **Write waits for readers to finish.**
- **Readers wait for writer to finish.**

---
