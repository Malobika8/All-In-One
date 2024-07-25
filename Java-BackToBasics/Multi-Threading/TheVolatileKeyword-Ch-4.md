## How does the usage of volatile come into play?

Suppose there are two threads. A thread interacts with a CPU & CPU in turn interacts with the Main Memory or RAM. There's a Cache in between
which helps us in reducing the access time. We know that it is far more efficient for a CPU to access data from the Cache than from the Main
Memory. Cache gives us fast data access time. 

<img width="1150" alt="Screenshot 2024-07-25 at 2 11 00 PM" src="https://github.com/user-attachments/assets/798ad9b2-4c2e-4f87-9f0b-8daf675dea4e">

Suppose there's a shared variable(multiple threads try to access it & work on it) that exists in memory.
The shared variable is a Boolean flag variable & is set to **True** initially. Now, what happens is that both these threads 
don't directly read from the Memory. They have their own Cache & all these threads read the value of the shared variable locally from their 
Cache. Now, the problem that might happen is, if let's say, "thread-2" changes the value of the flag to **False**. It won't directly update 
it to the RAM. It would first update it in its local Cache. 

<img width="1078" alt="Screenshot 2024-07-25 at 2 13 15 PM" src="https://github.com/user-attachments/assets/ee195b85-c8f8-4133-b008-559b7890c668">

In such case, we can see that it updates the flag variable to **False** in Cache but the other thread still can see the value of the variable as 
**True** because it is not updated in its local Cache as well as the Main Memory. It takes some time for this value of the Cache to be 
propagated to the Main Memory as **False**. But, we can see, that "thread-1" still doesn't have any visibility that the flag is actually changed 
to **False**.

<img width="1133" alt="Screenshot 2024-07-25 at 2 16 00 PM" src="https://github.com/user-attachments/assets/c13939d5-bcd3-4546-b76c-61c6294fddd9">

Now, to get rid of this problem, we introduce the *volatile* keyword. We can declare the same variable as *volatile*. These threads then no 
longer read from the Cache or the local copy. They can directly read from the Main memory. As a result, if "thread-2" changes the flag 
to **False**, "thread-1" will have access to it.

<img width="1136" alt="Screenshot 2024-07-25 at 2 18 47 PM" src="https://github.com/user-attachments/assets/72f45cd1-e049-4fda-beb8-1d96ad6eb3ea">

Just in case, let's say there's a status flag that is constantly getting updated by multiple threads & based on the status flag, the other 
threads are doing some work. The condition of the status flag will actually direct how the threads will behave as all the threads need to have 
a consistent state of that particular variable.






