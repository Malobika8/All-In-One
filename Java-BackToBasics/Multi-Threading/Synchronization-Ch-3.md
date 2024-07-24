# Synchronization

• Threads share the same memory space, i.e. they can share resources (objects)
• However, there are critical situations where it is desirable that only one thread at a time has access to a shared resource.

Let's create a "Stack" class.

#### Note: In "**java.lang.Thread**", there's a method called *sleep()* that takes a parameter. This basically delays the thread for the time specified.

<img width="576" alt="Screenshot 2024-07-24 at 7 18 16 PM" src="https://github.com/user-attachments/assets/b5793e84-7db7-44cc-848e-d23dece23d1a">

"Main" class. Create two threads - one to "push" and another to "pop".

<img width="579" alt="Screenshot 2024-07-24 at 7 22 03 PM" src="https://github.com/user-attachments/assets/87c8802a-6fcf-4e24-a06f-3543f785653f">

Since these are two different separate threads, we don't know which one will be called first i.e. what the order will be.

Let's try to run and see if we face any issue.

<img width="559" alt="Screenshot 2024-07-24 at 7 26 04 PM" src="https://github.com/user-attachments/assets/33fed0bd-f300-4fdd-bf6f-4dde9f3c81bd">

So, what we can infer from this is there arise cases where we cannot allow multiple threads(to run parallely) to access a resource at a time.
We need to ensure that resources(here "push" & "pop) that are changing the state of the object are thread safe. We need to devise a methodology
to keep it thread safe.

We can put the shared resources to "synchronized" block.

#### But what is the lock that will help in understanding which thread would get access?

In Java, every object can be used as a lock.

<img width="568" alt="Screenshot 2024-07-24 at 7 39 50 PM" src="https://github.com/user-attachments/assets/02b61d1e-d420-4738-a864-d63cd96c1ad5">

So, whichever thread has access to this lock will enter the synchronized block.

**Note:** *If a particular synchronized method has a lock & that lock restricts access to other synchronized blocks as well, all the access to the 
synchronized methods will be blocked for all other threads that doesn't have that particular lock.*



