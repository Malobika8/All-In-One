# Thread Creation

A thread in Java is represented by an object of the Thread class. 

Creating threads is achieved in one of two ways:
   
1. Extending the "java.lang.Thread" class: "Thread" class has a *run()* method that needs to be overridden.

   <img width="845" alt="Screenshot 2024-07-24 at 11 45 54 AM" src="https://github.com/user-attachments/assets/cd7eca94-26e1-43f6-bed5-d6577fb7a0c3">
   <img width="851" alt="Screenshot 2024-07-24 at 11 51 46 AM" src="https://github.com/user-attachments/assets/0549e15d-52a9-4a4d-8314-b0ef3b7a65c6">
   <img width="581" alt="Screenshot 2024-07-24 at 11 53 22 AM" src="https://github.com/user-attachments/assets/8bcd0d0b-771b-447a-96fd-7ab2639a7945">

   The *start()* method doesn't start the thread immediately. It is an asynchronous method and it returns immediately. We don't know when the prgram
   starts and it is mostly up to the JVM. *start()* notifies JVM that the user wants to start the thread. JVM, on the other hand,  whenever
   appropriate, calls the *run()* method that we just implemented.

   There is no order (for thread execution) that is followed. We can also notice that the main thread exists. Even then, the program didn't terminate
   and it allowed the other thread to run. This is because "thread1" was a user thread.

   #### Points to note:
   - thread1 is the child thread of the main thread as it is spawned from the same.
   - The program might terminate once all the user threads finish executing. It is up to the JVM whether to allow the daemon thread to run
     or terminate abruptly
   - Create a daemon thread only to serve the functionality of the user thread. There's a flag that is initially set to false.
  
     <img width="848" alt="Screenshot 2024-07-24 at 12 19 20 PM" src="https://github.com/user-attachments/assets/6c8b7211-e2ba-4600-ad5d-96ea859342ef">

     To make the thread a daemon thread, we need to set it before we start the thread.

     <img width="853" alt="Screenshot 2024-07-24 at 12 20 53 PM" src="https://github.com/user-attachments/assets/46cf3888-ccdf-4975-a5e4-e45a3ec00f41">

     We can associate a name to a thread. For that, we need to override another method from "Thread" class.

     <img width="852" alt="Screenshot 2024-07-24 at 12 25 10 PM" src="https://github.com/user-attachments/assets/a65c22ab-a4cc-4a4f-b1ad-62f8242f28fe">

     There's a static method (*currentThread()*) in the "Thread" class that returns us the instance of the thread object that is currently running.

     <img width="861" alt="Screenshot 2024-07-24 at 12 25 31 PM" src="https://github.com/user-attachments/assets/79407683-bbca-456c-8b3b-b0e624532d31">
     <img width="876" alt="Screenshot 2024-07-24 at 12 35 52 PM" src="https://github.com/user-attachments/assets/aaddc570-3c0e-414a-85ba-ca08c324d3c5">

2. Implementing the "java.lang.Runnable" Interface:

   Runnable interface is a Functional interface as it has only 1 abstract method.

   <img width="590" alt="Screenshot 2024-07-24 at 12 56 34 PM" src="https://github.com/user-attachments/assets/e7c89953-0456-4081-8b29-0493f3a09a36">

   We again have to provide an implementation to the *run()* method.
   
   <img width="857" alt="Screenshot 2024-07-24 at 1 02 00 PM" src="https://github.com/user-attachments/assets/1871c763-8984-4468-83ef-7881956d0293">
   <img width="855" alt="Screenshot 2024-07-24 at 1 03 33 PM" src="https://github.com/user-attachments/assets/8c61419e-a9fc-4e14-b976-debafce35d93">
   <img width="571" alt="Screenshot 2024-07-24 at 1 05 45 PM" src="https://github.com/user-attachments/assets/23f345e3-165c-4c05-8cd1-dc5820fd8acb">

### Let's analyze the reason behind 2 ways of creating Thread.

If we look closely, the "Thread" class also implements "Runnable". 

#### Then why does it ask us to provide an object of Runnable?

Also, the "Thread" class itself has a *run()* method which we can use. Why can't we just use it?

<img width="855" alt="Screenshot 2024-07-24 at 5 45 44 PM" src="https://github.com/user-attachments/assets/6f2b7696-255c-4970-851d-0baf340ff927">

The *run()* method does nothing. It has an object(named "target"/"task"(lastest)) of the Runnable interface and initially, it is set to null.

<img width="803" alt="Screenshot 2024-07-24 at 5 47 58 PM" src="https://github.com/user-attachments/assets/5553a066-ea49-4a0e-967f-75a2009d4343">
<img width="603" alt="Screenshot 2024-07-24 at 5 46 40 PM" src="https://github.com/user-attachments/assets/12f64ac1-5c95-404e-8fd5-c6af0e86c23e">

#### What should we do to call the *target.run()* method?

We can ensure that the "target"/"task" object is not null. When we pass the Runnable instance, it is set to "target"/"task".

<img width="965" alt="Screenshot 2024-07-24 at 5 57 40 PM" src="https://github.com/user-attachments/assets/fbbf1b7c-e856-4837-81a0-30dfdb0f0427">
<img width="949" alt="Screenshot 2024-07-24 at 5 57 47 PM" src="https://github.com/user-attachments/assets/d47b8ad6-645b-4df9-aa42-33da8c94f05c">
<img width="934" alt="Screenshot 2024-07-24 at 5 55 55 PM" src="https://github.com/user-attachments/assets/63fec8b5-877d-49b0-9456-170802e1abfe">
<img width="934" alt="Screenshot 2024-07-24 at 5 56 22 PM" src="https://github.com/user-attachments/assets/56610a88-bcbe-4149-a361-6043dc08e6a9">

and "target"/"task".*run()* is nothing but the implementation that is provided by us. So, the *run()* of the object passed is called.

<img width="965" alt="Screenshot 2024-07-24 at 6 01 17 PM" src="https://github.com/user-attachments/assets/df2b36d1-6c05-4b0e-b4bd-1f2ca136029b">

**Hence, we can either extend Thread directly and override the *run()* method.**

**OR,**

**We can implement Runnable and trigger the thread using the "Thread" class.**

## Note: 

If we extend "Thread" then we won't be able to extend any other class as mutliple inheritence in not supported in Java. This will limit us.
So, it is always better to implement "Runnable".

# To sum up

<img width="1145" alt="Screenshot 2024-07-24 at 7 09 06 PM" src="https://github.com/user-attachments/assets/1e8e9c5a-99c8-451c-bf1f-9b6517e4ed6c">
<img width="1063" alt="Screenshot 2024-07-24 at 7 10 20 PM" src="https://github.com/user-attachments/assets/1db18677-9008-4acf-a60a-d98f9fed8630">



     
  

   



   
