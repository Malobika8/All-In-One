# Synchronization

• Threads share the same memory space, i.e. they can share resources (objects)
• However, there are critical situations where it is desirable that only one thread at a time has access to a shared resource.

Let's create a "Stack" class.

#### Note: In "**java.lang.Thread**", there's a method called *sleep()* that takes a parameter. This basically delays the thread for the time specified.

<img width="576" alt="Screenshot 2024-07-24 at 7 18 16 PM" src="https://github.com/user-attachments/assets/b5793e84-7db7-44cc-848e-d23dece23d1a">

"Main" class. Create two threads - one to "push" and another to "pop".

<img width="579" alt="Screenshot 2024-07-24 at 7 22 03 PM" src="https://github.com/user-attachments/assets/87c8802a-6fcf-4e24-a06f-3543f785653f">

Since these are two different separate threads, we don't know which one will be called first i.e. what the order will be.

Let's try to run and see if we face any issues.

<img width="559" alt="Screenshot 2024-07-24 at 7 26 04 PM" src="https://github.com/user-attachments/assets/33fed0bd-f300-4fdd-bf6f-4dde9f3c81bd">

So, what we can infer from this is there arise cases where we cannot allow multiple threads(to run parallelly) to access a resource at a time.
We need to ensure that resources(here "push" & "pop) that are changing the state of the object are thread-safe. We need to devise a methodology
to keep it thread-safe.

We can put the shared resources into a "synchronized" block.

#### But what is the lock that will help in understanding which thread would get access?

In Java, every object can be used as a lock.

<img width="568" alt="Screenshot 2024-07-24 at 7 39 50 PM" src="https://github.com/user-attachments/assets/02b61d1e-d420-4738-a864-d63cd96c1ad5">

So, whichever thread has access to this lock will enter the synchronized block.

**Note:** *If a particular synchronized method has a lock & that lock restricts access to other synchronized blocks as well, all the access to the synchronized methods will be blocked for all other threads that don't have that particular lock.*

We are currently enclosing the entire method in a block. Instead of this, we can also declare the method itself as synchronized.

<img width="547" alt="Screenshot 2024-07-25 at 9 57 46 AM" src="https://github.com/user-attachments/assets/f93c2270-f8ec-4edf-bd90-a8fb6cdc48d5">

The compiler TRANSLATES the above to this,

<img width="549" alt="Screenshot 2024-07-25 at 9 59 44 AM" src="https://github.com/user-attachments/assets/2e9b567d-805d-49e1-82a5-30aab4de46cb">

So, for all the synchronized methods in the Class, the lock will be the current instance ("**this**") of the class.

Note: Whenever we use a synchronized block, we have to use an explicit lock. In the case of a synchronized method, we don't require a lock.

### What would happen in the case of static methods though?

We synchronize on the class lock itself. We cannot use "this" in a static method.

<img width="550" alt="Screenshot 2024-07-25 at 10 08 55 AM" src="https://github.com/user-attachments/assets/0064274f-d0fc-4fbf-a47e-4fd849287de9">
<img width="563" alt="Screenshot 2024-07-25 at 10 08 46 AM" src="https://github.com/user-attachments/assets/c9c718f1-c2b8-46c2-8466-fb71188977fc">

## Rules of Synchronization :
* A thread must acquire the object lock associated with a shared resource before it can enter the shared resource.
* The runtime system ensures that no other thread can enter a shared resource if another thread already holds the object lock associated
  with it.
* If a thread cannot immediately acquire the object lock, it is blocked, i.e., it must wait for the lock to become available.
* When a thread exits a shared resource, the runtime system ensures that the object lock is also relinquished. If another thread is waiting
  for this object lock, it can try to acquire the lock in order to gain access to the shared resource.
* It should be made clear that programs should not make any assumptions about the order in which threads are granted ownership of a lock.

## Synchronized Blocks :
* Whereas the execution of synchronized methods of an object is synchronized on the lock of the object, the synchronized block allows the      execution of arbitrary code to be synchronized on the lock of an arbitrary object.
* The general form of the synchronized statement is as follows:
  ```
  synchronized (object ref expression) { <code block> }
  ```
* The object ref expression must evaluate to a non-null reference value, otherwise a NullPointerException is thrown.

## Synchronized Methods:
* While a thread is inside a synchronized method of an object, all other threads that wish to execute this synchronized method or any other
  synchronized method of the object will have to wait.
* This restriction does not apply to the thread that already has the lock and is executing a synchronized method of the object.
* Such a method can invoke other synchronized methods of the object without being blocked.
* The non-synchronized methods of the object can always be called at any time by any thread.
  
## Static Synchronized Methods:
* A thread acquiring the lock of a class to execute a static synchronized method has no effect on any thread acquiring the lock on any         object of the class to execute a synchronized instance method.
* In other words, the synchronization of static methods in a class is independent from the synchronization of instance methods on objects of
  the class.
* A subclass decides whether the new definition of an inherited synchronized method will remain synchronized in the subclass.

## Race Condition
It occurs when two or more threads simultaneously update the same value(stackTopIndex) and, as a consequence, leave the value in an undefined
or inconsistent state.

# Summary:
A thread can hold a lock on an object :
• By executing a synchronized instance method of the object. (this)
• By executing the body of a synchronized block that synchronizes on the object. (this)
• By executing a synchronized static method of a class or a block inside a static method (in which case, the object is the Class object        representing the class in the JVM)


