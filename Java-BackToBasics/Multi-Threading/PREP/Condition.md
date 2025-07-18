## ✅ What is a `Condition` in Java?

A `Condition` is like an advanced version of `wait()` and `notify()` — but it's used **with `ReentrantLock`** instead of `synchronized`.

---

### 🔁 Analogy:

| With `synchronized` | With `ReentrantLock` + `Condition` |
| ------------------- | ---------------------------------- |
| `wait()`            | `condition.await()`                |
| `notify()`          | `condition.signal()`               |
| `notifyAll()`       | `condition.signalAll()`            |

---

### 🔧 Why do we use `Condition`?

Because `ReentrantLock` doesn’t support `wait()`/`notify()`, it provides `Condition` objects to achieve the **same coordination** — but with **more flexibility**.

You can:

* Create **multiple `Condition` objects** on the same lock (like multiple waiting queues)
* Control **which group of threads to wake up**

---

### ✅ Code Syntax:

```java
Lock lock = new ReentrantLock();
Condition condition = lock.newCondition();

lock.lock();
try {
    condition.await();     // like wait()
    condition.signal();    // like notify()
    condition.signalAll(); // like notifyAll()
} finally {
    lock.unlock();
}
```

---

### 🔹Real-World Use Case:

Let’s say:

* You have a `MessageQueue`
* **Producers** add messages
* **Consumers** wait for messages

You can use one `Condition` to:

* **Wait** when queue is empty
* **Signal** consumers when message is available

---

## ❌ Why `t.wait()` doesn’t work with `ReentrantLock`:

### 1. `wait()` is tied to **intrinsic locks** (i.e., `synchronized`)

* You can only call `wait()` on an object **that the thread currently holds a monitor lock on**.
* That means: `wait()` works only **inside a `synchronized(obj)` block**, not inside `lock.lock()`.

### 2. `ReentrantLock` doesn’t use object monitors

* `ReentrantLock` is part of the `java.util.concurrent.locks` package.
* It manages its own internal lock state — it **does not interact with the object's monitor**.
* So, calling `wait()` on an object in a `lock.lock()` block **will throw `IllegalMonitorStateException`** because the thread doesn't own the monitor lock of `t`.

---

### ✅ Correct Way: Use `Condition.await()` instead of `t.wait()`

```java
Lock lock = new ReentrantLock();
Condition condition = lock.newCondition();

lock.lock();
try {
    condition.await(); // ✅ Correct - this releases the ReentrantLock and waits
} catch (InterruptedException e) {
    e.printStackTrace();
} finally {
    lock.unlock();
}
```

---

## ✅ Summary Table:

| Concept         | `synchronized`            | `ReentrantLock`           |
| --------------- | ------------------------- | ------------------------- |
| Locking keyword | `synchronized`            | `lock.lock()`             |
| Wait method     | `obj.wait()`              | `condition.await()`       |
| Notify method   | `obj.notify()`            | `condition.signal()`      |
| Restrictions    | Must own monitor of `obj` | Must hold `ReentrantLock` |

---

## 🔹Scenario:

* Producer adds items to a shared queue
* Consumer takes items from the queue
* If the queue is **empty**, consumer waits
* If the queue is **full**, producer waits

---

## ✅ Complete Working Code (bounded buffer of size 1)

```java
import java.util.LinkedList;
import java.util.Queue;
import java.util.concurrent.locks.*;

public class Main {
    public static void main(String[] args) {
        SharedQueue sharedQueue = new SharedQueue(1); // Capacity = 1

        Runnable producer = () -> {
            for (int i = 1; i <= 5; i++) {
                sharedQueue.produce(i);
            }
        };

        Runnable consumer = () -> {
            for (int i = 1; i <= 5; i++) {
                sharedQueue.consume();
            }
        };

        Thread producerThread = new Thread(producer, "Producer");
        Thread consumerThread = new Thread(consumer, "Consumer");

        producerThread.start();
        consumerThread.start();
    }
}

class SharedQueue {
    private final Queue<Integer> queue = new LinkedList<>();
    private final int capacity;

    private final Lock lock = new ReentrantLock();
    private final Condition notFull = lock.newCondition();
    private final Condition notEmpty = lock.newCondition();

    SharedQueue(int capacity) {
        this.capacity = capacity;
    }

    public void produce(int item) {
        lock.lock();
        try {
            while (queue.size() == capacity) {
                System.out.println(Thread.currentThread().getName() + " waiting, queue is full.");
                notFull.await();
            }

            queue.offer(item);
            System.out.println(Thread.currentThread().getName() + " produced: " + item);

            // Signal one consumer thread
            notEmpty.signal();
        } catch (InterruptedException e) {
            e.printStackTrace();
        } finally {
            lock.unlock();
        }
    }

    public void consume() {
        lock.lock();
        try {
            while (queue.isEmpty()) {
                System.out.println(Thread.currentThread().getName() + " waiting, queue is empty.");
                notEmpty.await();
            }

            int item = queue.poll();
            System.out.println(Thread.currentThread().getName() + " consumed: " + item);

            // Signal one producer thread
            notFull.signal();
        } catch (InterruptedException e) {
            e.printStackTrace();
        } finally {
            lock.unlock();
        }
    }
}
```

---

### 🧠 Key Points:

* `await()` releases the lock and waits
* `signal()` wakes up a waiting thread (still needs to reacquire the lock)
* Always call `await()`/`signal()` **inside a `lock.lock()`/`unlock()` block**
* Use `while` not `if` for waiting (to avoid spurious wakeups)

---

### ✅ Sample Output:

```
Producer produced: 1
Consumer consumed: 1
Producer produced: 2
Consumer consumed: 2
...
```

