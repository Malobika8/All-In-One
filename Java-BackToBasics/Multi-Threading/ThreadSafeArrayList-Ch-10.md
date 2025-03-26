In Java, an **ArrayList** is **not thread-safe** by default, meaning if multiple threads modify it simultaneously, you might run into race conditions or `ConcurrentModificationException`. Let’s look at some simple ways to make an `ArrayList` thread-safe:

---

### 🚦 **1. Use `Collections.synchronizedList()`**

This method wraps the `ArrayList` with a synchronized list, making all operations thread-safe:

```java
import java.util.*;

public class SynchronizedArrayListExample {
    public static void main(String[] args) {
        List<Integer> list = Collections.synchronizedList(new ArrayList<>());

        // Adding elements from multiple threads
        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 5; i++) {
                list.add(i);
            }
        });

        Thread t2 = new Thread(() -> {
            for (int i = 5; i < 10; i++) {
                list.add(i);
            }
        });

        t1.start();
        t2.start();

        try {
            t1.join();
            t2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        // Synchronized access during iteration
        synchronized (list) {
            for (Integer i : list) {
                System.out.println(i);
            }
        }
    }
}
```

✅ **Pros:** Simple and effective.  
❌ **Cons:** You still need to explicitly synchronize when **iterating** over the list to avoid `ConcurrentModificationException`.

---

### ⚡ **2. Use `CopyOnWriteArrayList` (Best for Read-heavy Workloads)**

`CopyOnWriteArrayList` creates a new copy of the list every time you modify it, making reads very fast and inherently thread-safe without needing explicit synchronization.

```java
import java.util.concurrent.CopyOnWriteArrayList;

public class CopyOnWriteArrayListExample {
    public static void main(String[] args) {
        CopyOnWriteArrayList<Integer> list = new CopyOnWriteArrayList<>();

        // Adding elements from multiple threads
        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 5; i++) {
                list.add(i);
            }
        });

        Thread t2 = new Thread(() -> {
            for (int i = 5; i < 10; i++) {
                list.add(i);
            }
        });

        t1.start();
        t2.start();

        try {
            t1.join();
            t2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        // No need to synchronize during iteration
        for (Integer i : list) {
            System.out.println(i);
        }
    }
}
```

✅ **Pros:** No need to synchronize while iterating, great for **read-heavy** use cases.  
❌ **Cons:** Costly for **write-heavy** workloads due to frequent copying.  

---

### ⚙️ **3. Use `ReentrantLock` for Fine-Grained Control**

If you want more control, you can manually synchronize using a `ReentrantLock`:

```java
import java.util.*;
import java.util.concurrent.locks.ReentrantLock;

public class LockBasedArrayListExample {
    private final List<Integer> list = new ArrayList<>();
    private final ReentrantLock lock = new ReentrantLock();

    public void add(int value) {
        lock.lock();
        try {
            list.add(value);
        } finally {
            lock.unlock();
        }
    }

    public void printList() {
        lock.lock();
        try {
            for (Integer i : list) {
                System.out.println(i);
            }
        } finally {
            lock.unlock();
        }
    }

    public static void main(String[] args) {
        LockBasedArrayListExample example = new LockBasedArrayListExample();

        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 5; i++) {
                example.add(i);
            }
        });

        Thread t2 = new Thread(() -> {
            for (int i = 5; i < 10; i++) {
                example.add(i);
            }
        });

        t1.start();
        t2.start();

        try {
            t1.join();
            t2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        example.printList();
    }
}
```

✅ **Pros:** Full control over locking.  
❌ **Cons:** Requires more boilerplate code.  

---

### 🌟 **When to Use What?**

- ✅ **Use `Collections.synchronizedList()`** if you just want a quick and simple solution.  
- ✅ **Use `CopyOnWriteArrayList`** if you have **more reads than writes**.  
- ✅ **Use `ReentrantLock`** if you want **fine-grained control** over locking and concurrency.  

