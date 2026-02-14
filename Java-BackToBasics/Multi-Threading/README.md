## Process

A process is an independent program in execution.
It has its own memory space and system resources.
A process can contain one or more threads.

## Thread

A thread is the smallest unit of execution within a process.
Multiple threads inside a process share the same memory and resources but execute different tasks concurrently.

## Race conditions in Java can be prevented using:

1️⃣ synchronized keyword

- Can be applied on method or block
- Ensures only one thread executes the critical section at a time
- Uses intrinsic monitor lock

2️⃣ Explicit Locks (ReentrantLock)

From java.util.concurrent.locks
- More flexible than synchronized
- Supports:
  - tryLock()
  - fairness policy
  - interruptible locks
- Must manually release lock in finally block

3️⃣ Atomic Classes

From java.util.concurrent.atomic
- AtomicInteger
- AtomicLong
- AtomicReference

They use CAS (Compare-And-Swap) internally. Very efficient, no blocking.

4️⃣ Using Concurrent Collections

- Instead of: HashMap Use: ConcurrentHashMap
- Instead of: ArrayList Use: CopyOnWriteArrayList

5️⃣ Immutability

If objects are immutable:

- No shared mutable state
- No race condition
  Example: String, Wrapper classes

Race conditions can be avoided by ensuring proper synchronization, using lock mechanisms, atomic variables, concurrent collections, or by designing immutable objects.
