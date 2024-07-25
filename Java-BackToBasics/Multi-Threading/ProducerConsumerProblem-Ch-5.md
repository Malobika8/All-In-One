# Producer Consumer Problem

Consider a Queue and list of threads. One group of threads try to push items to the Queue and another group tries to pull items out of the Queue.

<img width="999" alt="Screenshot 2024-07-25 at 6 28 34 PM" src="https://github.com/user-attachments/assets/3163ae63-50dc-4b71-84fa-afb186ab3683">

* Pushing items is possible only if space for there's atleast 1 item in the Queue i.e. Queue is not full.

  <img width="947" alt="Screenshot 2024-07-25 at 6 29 01 PM" src="https://github.com/user-attachments/assets/2dc347e9-241f-4e5b-bd2b-648b077c64bd">

* Removing item is possible only if there's atleast 1 item in the Queue i.e. Queue is not empty.

  <img width="951" alt="Screenshot 2024-07-25 at 6 29 20 PM" src="https://github.com/user-attachments/assets/13165b2c-f056-4682-a95c-7bd42c9110e7">

Consider the following,

<img width="826" alt="Screenshot 2024-07-25 at 6 37 11 PM" src="https://github.com/user-attachments/assets/5521dd91-1b26-4e36-ae84-87bc96ea3dd7">

We can observe two things
- If (**q.size == capacity**), the thread needs to wait till atleast 1 item from the Queue is removed so that "push" operation can be done.
- If (**q.size == 0**), the thread needs to wait till atleast 1 item is added so that "remove" operation can be done.

Let's consider the "remove" scenario.

The "remover-thread" has access to the code block but cannot execute the code coz the size of the Queue is 0 & it has nothing to remove. Since
it has access to this critical section block, the other threads (even the "adder-threads" who can add items to the Queue to potentially
unblock this "remover-thread") are also blocked as they don't have access to the Queue currently. 

### What should the "remover-thread" do then?

It has to wait till any other "added-threads" adds any item to the Queue. This is because if any "adder-thread" adds any item to the Queue, this
particular thread would be free to remove an item from the Queue.

Object class has three methods - *wait(), notify() & notifyAll()*

The "remover-thread" has to wait and reliquish the lock. If a thread waits, then other threads get a chance to access the critical section.
It will wait till the Queue has some item to be removed. 

### But how will it know?

It has to be notified about the same. The "adder-thread" would notify once an item is pushed to the Queue. *notifyAll()* notifies all the threads
that are in waiting state.

<img width="821" alt="Screenshot 2024-07-25 at 6 51 21 PM" src="https://github.com/user-attachments/assets/a3bf36f1-9fc5-488a-8ec0-4d7c0aa795a9">

The same is true for "adder" as well.

<img width="820" alt="Screenshot 2024-07-25 at 6 53 28 PM" src="https://github.com/user-attachments/assets/2e82bd8c-93e2-452c-824f-665f74bca923">

There's one slight problem though.

Suppose an "adder-thread" comes and gets lock to the synchronized block only to find out that the Queue is already full. So, it goes into waiting
state and relinquishes the lock. Instantly, say another "adder-thread" gets the lock and find out that the Queue is full. Similar to the 
previous one, it also goes to the waiting state and relinquishes the lock. 

<img width="1135" alt="Screenshot 2024-07-25 at 7 08 22 PM" src="https://github.com/user-attachments/assets/90481981-d5dd-49f4-8b14-1e2f15644cdf">

Next time, suppose a "remover-thread" gets hold of the lock. It removes an item and notifies all the waiting threads. 

<img width="1146" alt="Screenshot 2024-07-25 at 7 08 57 PM" src="https://github.com/user-attachments/assets/df4fa702-33c9-4b37-9253-eb29380f757a">

Now, suppose the first thread gets hold of the lock again and adds an item to the Queue. 

<img width="1148" alt="Screenshot 2024-07-25 at 7 10 41 PM" src="https://github.com/user-attachments/assets/b5d81172-7226-49ac-b089-80fbea55da39">

Following that, suppose the second "adder-thread" gets the lock but it finds out that the Queue is again full because of which push is not possible.

<img width="1148" alt="Screenshot 2024-07-25 at 7 11 56 PM" src="https://github.com/user-attachments/assets/ea5c3363-7e90-4ea7-b263-240c6aa5c363">

So, it is always better to check the condition before actually doing the operation(push/remove).

<img width="1110" alt="Screenshot 2024-07-25 at 7 13 27 PM" src="https://github.com/user-attachments/assets/a51e9177-25ad-4594-a548-f6bfbad9d523">





