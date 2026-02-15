# What Is a Semaphore?

A **Semaphore** controls **how many threads can access a resource at the same time**. It works using **permits**. Think of it like:
"Only N threads are allowed inside this room at once."

### Basic Example

```java
Semaphore semaphore = new Semaphore(3);
```

This means:

* Only **3 threads** can access the critical section simultaneously.
* If a 4th thread comes → it waits.

## Core Methods

```java
semaphore.acquire();   // take a permit (may block)
semaphore.release();   // return permit
```

If no permits are available → `acquire()` blocks.

### Real-World Example

Imagine:

* Database connection pool of size 10
* Only 10 threads can use DB at a time

You use:

```java
Semaphore dbConnections = new Semaphore(10);
```

Before using DB:

```java
dbConnections.acquire();
```

After done:

```java
dbConnections.release();
```

### Difference from synchronized

| synchronized          | Semaphore                |
| --------------------- | ------------------------ |
| Only 1 thread allowed | Multiple threads allowed |
| Implicit locking      | Explicit permit control  |
| Block-level           | Resource-based control   |

Semaphore can be:

```java
new Semaphore(3, true);
```

Second parameter = fairness

If true → FIFO order of thread access
If false → no guarantee (better performance)

## Where It's Used in Real Systems

* Rate limiting APIs
* DB connection pool
* Limiting concurrent file access
* Restricting expensive resource usage

# Question: If I create:

```java
Semaphore semaphore = new Semaphore(1);
```

What does it behave like?


