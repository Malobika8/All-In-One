# Consider the producer consumer code

```
import java.util.*;
class Main {

    static Queue<Integer> queue = new LinkedList<>();
    static Object obj = new Object();

    public static void main(String[] args) {

        Runnable producer = () -> {
            int val = 1;
            while (true) {
                synchronized (obj) {
                    while (queue.size() == 5) {
                        try { obj.wait(); } 
                        catch (InterruptedException e) { e.printStackTrace(); }
                    }
                    queue.add(val);
                    System.out.println("Produced: " + val);
                    val++;
                    obj.notifyAll();
                }
            }
        };

        Runnable consumer = () -> {
            while (true) {
                synchronized (obj) {
                    while (queue.isEmpty()) {
                        try { obj.wait(); } 
                        catch (InterruptedException e) { e.printStackTrace(); }
                    }
                    int val = queue.remove();
                    System.out.println("Consumed: " + val);
                    obj.notifyAll();
                }
            }
        };

        new Thread(producer).start();
        new Thread(consumer).start();
    }
}
```

# Producer-Consumer with `BlockingQueue`

```java
import java.util.concurrent.*;

class Main {
    public static void main(String[] args) {

        // Shared bounded buffer with capacity 5
        BlockingQueue<Integer> queue = new ArrayBlockingQueue<>(5);

        Runnable producer = () -> {
            int val = 1;
            try {
                while (true) {
                    queue.put(val); // waits automatically if queue is full
                    System.out.println("Produced: " + val);
                    val++;
                    Thread.sleep(500); // simulate work
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        };

        Runnable consumer = () -> {
            try {
                while (true) {
                    int val = queue.take(); // waits automatically if queue is empty
                    System.out.println("Consumed: " + val);
                    Thread.sleep(1000); // simulate work
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        };

        new Thread(producer).start();
        new Thread(consumer).start();
    }
}
```

# 🔹 Key Points

1. `ArrayBlockingQueue<>(5)` → buffer of size 5
2. `queue.put()` → waits automatically if queue is full
3. `queue.take()` → waits automatically if queue is empty
4. No need for `synchronized`, `wait()`, or `notifyAll()`
5. Very safe, less error-prone, and **interview-friendly**

`BlockingQueue` is **preferred over manual wait/notify**, especially for production systems — it avoids deadlocks and simplifies your code drastically.

## Blocking Behavior

* `ArrayBlockingQueue` (and other `BlockingQueue` implementations like `LinkedBlockingQueue`) **automatically handle waiting**.
* If you call:

  ```java
  queue.put(item);
  ```

  * If the queue is **full**, the thread **blocks** until space becomes available.

  ```java
  queue.take();
  ```

  * If the queue is **empty**, the thread **blocks** until an item is available.

No need for `wait()` or `notify()` — it’s built into the queue.

## Methods**

* **Blocking Methods** (wait/block automatically):

| Method                               | Behavior                                      |
| ------------------------------------ | --------------------------------------------- |
| `put(E e)`                           | Blocks if full, then inserts element          |
| `take()`                             | Blocks if empty, then removes element         |
| `offer(E e, long timeout, TimeUnit)` | Tries to insert, waits up to timeout if full  |
| `poll(long timeout, TimeUnit)`       | Tries to remove, waits up to timeout if empty |

* **Non-blocking Methods** (behave like normal queues, return immediately):

| Method       | Behavior                                        |
| ------------ | ----------------------------------------------- |
| `add(E e)`   | Throws exception if queue full                  |
| `offer(E e)` | Returns `false` if queue full                   |
| `remove()`   | Throws exception if queue empty                 |
| `poll()`     | Returns `null` if queue empty                   |
| `peek()`     | Looks at head without removing, `null` if empty |

> **Key difference:** `put()`/`take()` **block** threads until the operation can succeed, whereas `add()`/`remove()`/`offer()`/`poll()` do **not block**.

## Why BlockingQueue is better than manual wait/notify

1. You **don’t need synchronized/wait/notify**.
2. Avoids common mistakes like **missed notify or deadlocks**.
3. Scales easily to **multiple producers and consumers**.
4. More **readable and maintainable** code.





