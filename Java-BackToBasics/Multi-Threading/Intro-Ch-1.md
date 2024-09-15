# Multitasking

Multitasking allows several activities to occur concurrently on the computer. In terms of computers, it's about running different programs 
simultaneously at a time.

* Process-based Multitasking (Example: playing chess - watching movies - surfing the internet all at once): Multiple processes running parallelly.
* Thread-based Multitasking (Example: typing something in ms-word with autocorrect activated): It is about multitasking
  within a particular program itself. This is when Thread comes into the picture. Multiple threads run within a program.  

### Difference between a Thread and a Process?

Since multiple threads work for the same program, they share the same Address Space. Hence, switching between two threads is less expensive 
than switching between two processes.

### Threads vs Process :
• Two threads share the same address space
• Context switching between threads is usually less expensive than between processes.
• The cost of communication between threads is relatively less.

### Why MultiThreading?

(*We don't want to wait for one particular task to complete. It would be too time-consuming.*)

* In a single-threaded environment, only one task at a time can performed.
* CPU cycles are wasted, for example, when waiting for user input.
* Multitasking allows idle CPU time to be put to good use.

### Threads

* We don't need to explicitly create the main thread. It is automatically created.
* A thread is an independent sequential path of execution within a program.
* Many threads can run concurrently within a program.
* At runtime, threads in a program exist in a common memory space and can, therefore, share both the data and code (i.e., they are
  lightweight compared to processes).

### 3 important concepts related to Multithreading in Java

* Creating threads and providing the code that gets executed by a thread.
* Accessing common data and code through synchronization
* Transitioning between thread states.

### The Main Thread :
* When a standalone application is run, a user thread is automatically created to execute the main() method of the application. This thread
  is called the main thread.
* If no other user threads are spawned, the program terminates when the main() method finishes executing.
* All other threads, called child threads, are spawned from the main thread.
* The main() method can then finish, but the program will keep running until all user threads have been completed.
* The runtime environment distinguishes between user threads and daemon threads. Calling the setDaemon (boolean) method in the Thread class    marks the status of the thread as either daemon or user, but this must be done before the thread is started.
* As long as a user thread is alive, the JVM does not terminate.
* A daemon thread is at the mercy of the runtime system: it is stopped if no more user threads are running, thus terminating the program.












