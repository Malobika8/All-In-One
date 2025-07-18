# What is ReentrantLock? How is it different from synchronized? When would you use one over the other?
- What ReentrantLock is
- How it compares to synchronized
- When you'd prefer it in real-world scenarios

### Sol:

`ReentrantLock` is a class that implements the `Lock` interface and provides an **explicit, flexible, and powerful locking mechanism**.
Unlike `synchronized`, where the JVM handles locking implicitly, with `ReentrantLock`:
* You **manually acquire** and **release** the lock using:

  ```java
  lock.lock();
  try {
     // critical section
  } finally {
     lock.unlock(); // must be done to avoid deadlocks
  }
  ```

| Feature                           | `synchronized`          | `ReentrantLock`                   |
| --------------------------------- | ----------------------- | --------------------------------- |
| Lock handling                     | Automatic               | Manual (`lock()` and `unlock()`)  |
| Interruptible                     | ❌ No                    | ✅ Yes (`lockInterruptibly()`)     |
| Timed waiting                     | ❌ No                    | ✅ Yes (`tryLock(timeout)`)        |
| Fairness (first come first serve) | ❌ No                    | ✅ Yes (optional constructor flag) |
| Condition variables               | ❌ Basic (`wait/notify`) | ✅ Advanced (`Condition` objects)  |

> Use `ReentrantLock` when:

* You need **timeout-based locking** (`tryLock()`).
* You need to **interrupt threads** waiting for a lock (`lockInterruptibly()`).
* You want **fair lock acquisition** (first come, first serve).
* You need **multiple condition queues** for better coordination.

---

# Hands-On

Convert your current `Account` class to use `ReentrantLock` instead of `synchronized`.
> 🎯 Keep the same deposit/withdraw logic, but replace `synchronized` with `lock.lock()` and `lock.unlock()`.

### Sol:

```
class Main {
   
    public static void main(String[] args) throws InterruptedException {
        List<Thread> list = new ArrayList<>();
        Account account = new Account(20000);
        
        Runnable credit = ()->{
            account.deposit(1000);
        };
        Runnable debit = ()->{
            account.withdraw(500);
        };
        
        for(int i=0;i<3;i++){
            Thread thread1 = new Thread(credit); 
            thread1.start();
            list.add(thread1);
        }
        for(int i=0;i<2;i++){
            Thread thread2 = new Thread(debit); 
            thread2.start();
            list.add(thread2);
        }
        
        for(Thread th:list)
            th.join();
            
        System.out.println(account.getBalance());
    }
}

class Account{
    
    private int balance;
    
    Lock lock = new ReentrantLock();
    
    Account(int balance){
        this.balance = balance;
    }
    
    public int getBalance(){
        return balance;
    }
    
    public void deposit(int amount){
        try{
            lock.lock();
            balance = balance+amount;
        }
        finally{
            lock.unlock();
        }
    }
    public void withdraw(int amount){
        try{
            lock.lock();
            balance = balance-amount;
        }
        finally{
            lock.unlock();
        }
    }
}
```

---

# What happens if you forget to call lock.unlock() in a method that throws an exception? What issue will it cause in a multithreaded program?

## Sol:

If you forget to call lock.unlock(), the thread that acquired the lock never releases it, even if it finishes or crashes.
As a result, other threads waiting for the lock will remain blocked indefinitely, causing a deadlock or thread starvation.

---

# What does tryLock(long timeout, TimeUnit unit) do in ReentrantLock, and when would you use it instead of lock()?

## Sol:

> The `tryLock(long timeout, TimeUnit unit)` method in `ReentrantLock` tries to acquire the lock, but only **waits for a limited time**.
> If the lock is not available within that time, it **returns `false`** instead of blocking the thread forever.


#### 🔹Use it when:

* You **don’t want threads to wait indefinitely**
* You have **alternative logic or fallback** if the lock isn’t acquired
* You want to avoid **deadlocks or thread starvation**

```java
if (lock.tryLock(1, TimeUnit.SECONDS)) {
    try {
        // critical section
    } finally {
        lock.unlock();
    }
} else {
    System.out.println("Could not acquire lock, doing something else.");
}
```

---

# Hands-on:

Write a class `Printer` with a `printDocument()` method that:

* Uses `ReentrantLock.tryLock(1, TimeUnit.SECONDS)`
* Prints the document if the lock is acquired
* Otherwise prints “Printer is busy”

Simulate two threads trying to print at the same time.

### Sol:

```
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;
import java.util.concurrent.TimeUnit;

class Main {
    public static void main(String[] args) throws InterruptedException {
        Printer printer = new Printer();

        Runnable print = () -> {
            printer.printDocument();
        };

        Thread t1 = new Thread(print);
        Thread t2 = new Thread(print);

        t1.start();
        t2.start();

        t1.join();
        t2.join();
    }
}

class Printer {
    private final Lock lock = new ReentrantLock();

    public void printDocument() {
        try {
            if (lock.tryLock(2, TimeUnit.SECONDS)) {
                try {
                    System.out.println(Thread.currentThread().getName() + " Printing...");
                    Thread.sleep(3000); // Simulate printing delay
                } finally {
                    lock.unlock();
                }
            } else {
                System.out.println(Thread.currentThread().getName() + " Printer is busy");
            }
        } catch (InterruptedException e) {
            System.out.println("Thread was interrupted");
        }
    }
}
```

---

# What is lockInterruptibly() in ReentrantLock and when would you use it?

### Sol:

The `lockInterruptibly()` method in `ReentrantLock` allows a thread to **acquire the lock unless it's interrupted** while waiting.
If the thread is interrupted while waiting to acquire the lock, it throws an **`InterruptedException`** and **does not continue waiting**.

#### Use `lockInterruptibly()` when:

* You want threads to **respond to interruptions** instead of waiting indefinitely.
* You need to implement **cancellable or timeout-sensitive operations**.
* You're writing **robust multithreaded systems** that shouldn’t get stuck waiting forever.

| Method                | Blocks forever?           | Can be interrupted? |
| --------------------- | ------------------------- | ------------------- |
| `lock()`              | ✅ Yes                     | ❌ No                |
| `lockInterruptibly()` | ✅ Yes (until interrupted) | ✅ Yes               |
| `tryLock(timeout)`    | ❌ No (waits fixed time)   | ❌ No                |

---

# Task:

**Write a program that:**

* Starts two threads.
* First thread acquires the lock and sleeps for 5 seconds.
* Second thread tries to `lockInterruptibly()`.
* Interrupt the second thread after 2 seconds and observe the behavior.

### Sol:

```
import java.util.concurrent.locks.ReentrantLock;
import java.util.concurrent.locks.Lock;

class Main {
    public static void main(String[] args) throws InterruptedException {
        Printer printer = new Printer();

        Runnable print = () -> {
            printer.printDocument();
        };

        Thread t1 = new Thread(print, "Thread-1");
        Thread t2 = new Thread(print, "Thread-2");

        t1.start();
        t2.start();

        // Give t1 time to acquire the lock
        Thread.sleep(2000);

        // Interrupt t2 so it stops waiting for the lock
        t2.interrupt();

        t1.join();
        t2.join();
    }
}

class Printer {
    private final Lock lock = new ReentrantLock();

    public void printDocument() {
        try {
            lock.lockInterruptibly(); // Can be interrupted while waiting
            try {
                System.out.println(Thread.currentThread().getName() + " acquired lock, Printing...");
                Thread.sleep(5000); // Simulate printing time
            } finally {
                lock.unlock();
            }
        } catch (InterruptedException e) {
            System.out.println(Thread.currentThread().getName() + " was interrupted while waiting for lock.");
        }
    }
}
```

---
















