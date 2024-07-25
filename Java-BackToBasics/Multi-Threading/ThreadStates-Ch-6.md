# Thread States

<img width="1032" alt="Screenshot 2024-07-25 at 7 15 58 PM" src="https://github.com/user-attachments/assets/a91b3675-1d83-40c3-a242-dcfc49d9fc0f">

### Note: 
- While sleeping, the thread doesn't relinquish the lock. While waiting, it does.
- Whenever a thread is notified, it does not directly jump into the runnable state. It has to fight for the lock i.e. it goes into
  "blocked-for-lock-aquisition" state.

In Java, there are some Enums. The "Thread" class provides the *getState()* method to determine the state of the current thread and the method returns
a constant of Type "Thread.State". The enum values are mentioned below.

<img width="1018" alt="Screenshot 2024-07-25 at 7 20 51 PM" src="https://github.com/user-attachments/assets/686cfbe8-ae93-4ef7-ba08-ec03580f1704">

Consider the following code segment,

<img width="812" alt="Screenshot 2024-07-25 at 7 23 30 PM" src="https://github.com/user-attachments/assets/e9b084d5-69cf-4d51-a565-5122fc20b733">

#### OUTPUT

<img width="568" alt="Screenshot 2024-07-25 at 7 25 38 PM" src="https://github.com/user-attachments/assets/5c7c04a7-a850-4450-b027-a1c9b89a1bc5">
<img width="572" alt="Screenshot 2024-07-25 at 7 25 52 PM" src="https://github.com/user-attachments/assets/59e93004-d78f-44d8-89bf-57eb10794a57">

## Running & Yielding

Whenever the *start()* method is called for a thread, it basically means that it is eligible for running. It waits for its turn to get CPU time.
Now, Thread Scheduler decides which thread to run & for how long. Whenever the thread gets scheduled to run by the CPU, from the "ready-to-run"
state, it transitions into the "running" state. 

When we call the *yield()* method, it basically tells the CPU to put the current running thread back into the "read-to-run" state & give other
threads a chance to run. It is an advisory made to the JVM which means that there is no guarantee that even if you call *yield()*, the
thread will transition at that point of time to the "ready-to-run" state. It is completely up to the JVM to decide whether it should push that
particular thread back to the "ready-to-run" state.

<img width="1061" alt="Screenshot 2024-07-25 at 7 26 48 PM" src="https://github.com/user-attachments/assets/c311a607-5e72-4ec3-bd4c-66572accf60f">

## Sleeping & Waking up

<img width="1068" alt="Screenshot 2024-07-25 at 7 33 13 PM" src="https://github.com/user-attachments/assets/7c26377e-5a04-4fac-aa77-91805305bc3f">

When we put a thread to sleep, it can be awakened only in 2 conditions.
- When the time has elapsed
- When it is interrupted by another thread. In that case, it won't wait for the time to elapse. It would go to the "ready-to-run" state & when it
  gets to the "running" state, it will throw an "**InterruptedException**". The same is the case with the *wait()* method.

## Waiting & Notifying

<img width="1063" alt="Screenshot 2024-07-25 at 7 37 42 PM" src="https://github.com/user-attachments/assets/af9525c4-fff6-49f2-a7fb-d5a3fe1e844c">
<img width="976" alt="Screenshot 2024-07-25 at 7 39 35 PM" src="https://github.com/user-attachments/assets/76a55d2a-a5c1-4e45-a69b-d4801d75fe1f">

### Wait: A thread in the Waiting-for-notification state can be awakened by the occurrence of any one of these three incidents.
* Another thread invokes the notify() method on the object of the waiting thread, and the waiting thread is selected as the thread to be
  awakened.
* The waiting thread times out.
* Another thread interrupts the waiting thread.

### Notify:
* Invoking the notify() method on an object wakes up a single thread that is waiting for the lock of this object.
* The selection of a thread to awaken is dependent on the thread policies implemented by the JVM.
* On being notified, a waiting thread first transits to the "Blocked-for-lock-acquisition" state to acquire the lock on the object, and not
  directly to the "Ready-to-run" state.
* The thread is also removed from the wait set of the object.

<img width="1140" alt="Screenshot 2024-07-25 at 7 44 22 PM" src="https://github.com/user-attachments/assets/1aa8f877-2944-429d-ac5d-c154a978a0b6">

## TimedOut

<img width="1096" alt="Screenshot 2024-07-25 at 7 45 27 PM" src="https://github.com/user-attachments/assets/0c526dac-cba7-4c73-acd0-30631ac3db34">

## Interrupted

<img width="1081" alt="Screenshot 2024-07-25 at 7 45 57 PM" src="https://github.com/user-attachments/assets/05fe3df2-79db-4187-a0e1-4d309c01935a">

### Difference between "TimedOut" and "Interrupted"

In "Interrupted", we get to know that this thread was interrupted by some other thread. However, in "TimedOut", we don't get to know whether 
it got "TimedOut" or it got "Notified" as there is no exception being thrown.

## Join
Consider the following code,

<img width="770" alt="Screenshot 2024-07-25 at 7 51 11 PM" src="https://github.com/user-attachments/assets/3cdc408b-b3f9-49dd-85a5-f9b043be8874">

In this case, our thread will have its own parallel way of executing and the "main" thread will have its own parallel way of executing.

<img width="570" alt="Screenshot 2024-07-25 at 7 58 47 PM" src="https://github.com/user-attachments/assets/e8b2544e-2772-48af-90b6-0edaf432f424">

Suppose we want to stop this asynchronous thing and we want this thread to first complete and then we want our "main" thread to run.
In that case, we can use the method, *thread.join()*.

<img width="773" alt="Screenshot 2024-07-25 at 7 53 43 PM" src="https://github.com/user-attachments/assets/4601c0a8-4b7d-4447-8ae4-947a94c183bf">

Whenever we call this *thread.join()*, "main" thread waits for the *run()* method of the thread(which we call to join) to complete first & then
our program starts executing. It basically blocks the "main" method to stop executing parallelly. It blocks the "main" thread from executing till
the other thread has finished executing.

<img width="569" alt="Screenshot 2024-07-25 at 7 57 18 PM" src="https://github.com/user-attachments/assets/ebb50e07-eae5-409f-90b8-7a89b9598f1d">

<img width="1058" alt="Screenshot 2024-07-25 at 8 00 21 PM" src="https://github.com/user-attachments/assets/6abaad53-2ad6-417c-ad60-9f456ab3ae88">

# Thread Priorities

<img width="1116" alt="Screenshot 2024-07-25 at 8 01 13 PM" src="https://github.com/user-attachments/assets/c7b707e4-55c0-4867-8f28-e7f4c175fecb">
<img width="1112" alt="Screenshot 2024-07-25 at 8 03 44 PM" src="https://github.com/user-attachments/assets/edfde3b2-1be1-4c12-93eb-ff376b68a967">

#### getPriority():

<img width="798" alt="Screenshot 2024-07-25 at 8 02 03 PM" src="https://github.com/user-attachments/assets/838e3338-dddf-479d-af0e-93b07547e01f">
<img width="574" alt="Screenshot 2024-07-25 at 8 02 54 PM" src="https://github.com/user-attachments/assets/e15687ad-cad8-4f63-bb11-e1f4c9f59501">

#### setPriority():

<img width="715" alt="Screenshot 2024-07-25 at 8 03 32 PM" src="https://github.com/user-attachments/assets/b6718776-e6fd-455f-a55c-d9acc529ac02">

# Thread Scheduler

<img width="1109" alt="Screenshot 2024-07-25 at 8 06 08 PM" src="https://github.com/user-attachments/assets/06dced49-0735-42ff-a5c6-2b1019ffc153">
















