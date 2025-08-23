# 🧵 Server Threads, Platform Threads & Virtual Threads

<img width="1024" height="1536" alt="image" src="https://github.com/user-attachments/assets/aadb6acd-40f0-4485-81c3-655d1fd110a8" />

---

## 1. How Tomcat works with **Thread-per-Request** model

* Tomcat (and most Java servers) traditionally follow **thread-per-request**:

  1. A client request comes in (say HTTP request).
  2. Tomcat assigns a **dedicated thread** from its thread pool to handle that request.
  3. The thread processes the request → runs servlets, filters, DB calls, etc.
  4. When the request completes, the thread returns to the pool.

* **Bottleneck**:

  * Threads are **heavyweight objects** at the OS level (backed by native resources like stack memory, kernel scheduling).
  * Each thread typically consumes **1 MB of memory** for stack by default.
  * If Tomcat has 200 threads → that’s \~200 MB stack usage just waiting.
  * When requests are waiting on I/O (DB, network, file), the thread is **blocked** but still occupies memory and counts towards limits.
  * Scaling beyond a few thousand threads becomes **very costly**.

---

## 2. Platform Threads (Traditional Java Threads)

* In Java, `Thread` is a **Platform Thread** (before JDK 19).
* Backed **1:1** with an OS thread → meaning each Java thread = one native OS thread.
* Expensive to create and manage:

  * **Creation cost** (kernel call, memory allocation).
  * **Context switching** between threads at OS level.
* Good for concurrency but not for **massive scale** (like 100k connections).

---

## 3. Virtual Threads (Project Loom, JDK 19+)

### Introduction

* **Virtual Thread** = lightweight thread managed by JVM, not OS.
* They are implemented **in user space**, on top of a small pool of carrier **platform threads**.
* **1M virtual threads** is possible on same machine where only \~2k platform threads were feasible.

### Difference from Platform Threads

| Aspect        | Platform Thread            | Virtual Thread                             |
| ------------- | -------------------------- | ------------------------------------------ |
| Backed by     | OS thread (1:1)            | JVM, multiplexed onto few platform threads |
| Creation cost | High (kernel call, \~1 MB) | Very low (\~KB stack, user mode)           |
| Blocking I/O  | Wastes OS thread           | JVM suspends & unmounts → no OS block      |
| Scalability   | Thousands                  | Millions                                   |

---

## 4. How Virtual Threads Work Internally

* **Mounting / Unmounting**:

  * A virtual thread runs code on a **carrier platform thread** (like renting a worker).
  * If the virtual thread hits a **blocking I/O** call:

    * JVM **parks/unmounts** it from the carrier thread.
    * Carrier thread is freed to run another virtual thread.
    * When I/O completes, the virtual thread is **mounted back** on any available carrier and resumes.

* This avoids wasting a native thread while waiting on I/O.

* **Carrying Thread (Carrier Thread)**:

  * A small set of real platform threads (like workers).
  * They “carry” virtual threads when they need CPU.
  * Acts as bridge between **JVM virtual threads** and **OS threads**.

---

## 5. Why Virtual Threads are Fast

* **Lightweight creation** (no kernel involvement).
* **No blocking waste**: waiting threads are unmounted.
* **Scheduler in JVM** (instead of kernel) → faster, less overhead.
* Ideal for servers that need to handle **massive concurrent connections**.

---

## 6. Why Virtual Threads are Best for I/O-bound, not CPU-bound

* **I/O-bound tasks**:

  * E.g., DB query, HTTP call, file read.
  * Virtual thread gets unmounted when waiting → high concurrency, low waste.
  * Can handle millions of open connections cheaply.
* **CPU-bound tasks**:

  * E.g., heavy computation (sorting, ML training).
  * Virtual thread can’t unmount, keeps consuming a carrier thread.
  * Too many CPU-bound virtual threads = starvation, because CPUs are limited.
  * Use **parallel streams / thread pools** for CPU-heavy tasks instead.

---

# ✅ Final Summary

* **Tomcat thread-per-request** = 1 thread per client request → bottleneck = limited by OS thread memory & blocking.
* **Platform threads** = Java `Thread`, 1:1 with OS thread, costly to scale.
* **Virtual threads** = lightweight, managed by JVM, mounted/unmounted on carrier threads.
* **Internals**: Virtual threads “borrow” a carrier thread, unmount when blocking, remount when ready.
* **Fast because**: cheap to create, no wasted blocking, managed in JVM.
* **Best for**: I/O-bound tasks (massive concurrency).
* **Not best for**: CPU-bound tasks (limited by number of cores).

---

