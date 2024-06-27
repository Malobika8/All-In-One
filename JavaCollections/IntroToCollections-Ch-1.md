# Collections Framework

*Collections* Class is part of Collections framework which contains some commonly used methods eg. **Collections.sort**.

<img width="1008" alt="Screenshot 2024-06-27 at 8 02 11 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/cbe631c7-e3a2-408a-8d99-a6d0e149041a">

There are multiple concrete Classes and Interfaces. Collections framework is nothing but implementation of DataStructures.

There exists already implementated Classes and Interfaces of frequently used Data Structures

<img width="1022" alt="Screenshot 2024-06-27 at 8 02 17 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/59607c56-bf9c-4a2f-96d1-a1874bb7a26b">

------
### Why did Java provide these though? We can implement these on own own.

They have provided so that we can focus on main logic rather than spending time on implementing these Data Structures. We just need to know how to use it.

------

------
### Collections is the root Interface of the collection hierarchy

It contains common methods for all the collections like *size, isEmpty, iterator* etc.

------

### There are 3 Interfaces:

------

### 1. List:
   * It is an ordered collection. It maintains insertion order.
   * It's like a Sequence
   * It has index which helps us access the elements at a particular position and even insert.

   <img width="712" alt="Screenshot 2024-06-27 at 8 35 18 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7d8b0114-f510-4f64-b141-d997526abdfe">

  ### Implementations:
  
  1. *ArrayList:*
     * Resizeable array implementation of the Interface.
     * It can increase its size on the fly.
     * It doubles the size once full. Note that both(old & new) the arrays are not maintained. Rather, it copies the info from first to            second. First one is later garbage collected.
     * It is Growable but limited.
     * This is more frequesntly used when we have high no of reads.
     * Random search is very fast because of Contiguous memory allocation.
    
       <img width="744" alt="Screenshot 2024-06-27 at 8 15 01 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a610040d-0e6e-4d43-a210-b62aa2d4c534">
       <img width="694" alt="Screenshot 2024-06-27 at 8 16 26 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/fbacc7b1-3c3a-486e-a469-17727f6e5501">
       <img width="995" alt="Screenshot 2024-06-27 at 8 46 40 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a365b8e4-f08c-42d5-b023-3407d6b9e0d1">

   2. *LinkedList:*
      * It is actually a doubly linked list Implementation.
      * It is not made of Contiguous memory allocation. They are connected with each other through pointers or references.
      * It maintains insertion order.
      * Random access is not fast. We always have to start from the beginning.
      * We can use LinkedList if we want to insert and delete the data again and again. In ArrayList, if we delete element, we have to              shift other elements. However, in LinkedList, we just need to change the references.
      * Use cases of LinkedList:
          * HashMap
          * Backward and Forward button in Chrome uses Stack and Stacks is implemented using LL.
      * LL supports LIFO as well.
 
        <img width="701" alt="Screenshot 2024-06-27 at 8 18 59 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/da17553f-14d7-41b5-bb41-2c771cd6cc69">

      ------
      ### Note: ArrayList and LL are not synchronized. They are not thread safe.
      ------
    
      <img width="734" alt="Screenshot 2024-06-27 at 8 28 16 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/29ea061c-cb90-4c40-b774-ba6145318542">

      ------
      ## Note: LL can also follow Queue Interface as it is also doubly ended.

      We can use LL as a Queue DS.
      ------

      <img width="580" alt="Screenshot 2024-06-27 at 9 22 50 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7e7d090b-9a0b-47d6-8d09-72093b391315">
      <img width="616" alt="Screenshot 2024-06-27 at 9 22 56 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/5c8670d8-0780-47f0-af78-ebfa6951756a">

      ### Imp Questions

      1. *Cycle in a LL*
      2. *LRU Cache.(Leetcode)*

      ------
      ### ArrayList & LinkedList overview:

      <img width="997" alt="Screenshot 2024-06-27 at 8 46 46 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ee1456cf-5c21-4ec5-93f5-6fe4d9c72775">
      ------

  3. *Vector:* If multiple people try to insert in ArrayList and LL, there will be a lot of issues as they are not Thread safe. That is          what happens when multiple threads try to access the same block which is the reason why Synchronization is important. This ensures          that the data is not corrupted.

     * This Class is just like ArrayList but along with that, it ensures Thread safety.
     * It can be used in a multi-threaded environment and the data won't be corrupted.
     * This class implements "growable" array of objects similar to ArrayList.
     * Vector is not generally used though as there are better DataStructure available that are much faster. This is a legacy DataStructure.

       ------
       Check this to know more: https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/package-summary.html
       ------

       <img width="1002" alt="Screenshot 2024-06-27 at 8 47 32 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d54e2ccd-dacb-4f77-aa74-414b61b85ee5">

   4. *Stack:*
      * This supports LIFO.
      * This is implemented using ArrayList or LL "behind the scene".
      * Stack extends Vector which means Stacks are also Thread safe.
      * *Stack.push()* doesn't have "synchronized" unlike other methods like pop, peek. This is because push calls "addElement()" method            internally that is synchronized which serves the purpose.

        <img width="621" alt="Screenshot 2024-06-27 at 8 36 41 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/de921163-9c02-4646-b64e-916bc66e5918">
        
------

### 2. Set: This need not necessarily have to be Ordered. By default, it's not ordered. It's a collection that doesn't contain any 
  duplicate elements. This only contains unique values.

   ------
   #### What is the use case of set? What is it best in?

   This is best in searching. Best case:O(1), worst:O(n)
   
   ------
  
   It is to be noted that Hashing is used behind the scenes.

   Lets try to add elements and print all the 3 sets. We can observe the order in which it prints the elements.

   <img width="651" alt="Screenshot 2024-06-27 at 9 02 06 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/adf52aaf-f7cd-414e-9b78-7e651e446681">
   
   * *HashSet* doesn't follow any order.
   * *LinkedHashSet* follows insertion order.
   * *TreeSet* sorts the elements in natural order. (searching/insertion: O(logn))
   
     <img width="719" alt="Screenshot 2024-06-27 at 9 05 21 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ba937926-5ab9-463e-871a-18a613bd7f27">
     <img width="668" alt="Screenshot 2024-06-27 at 9 10 47 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d20e4a12-2650-4b6e-85e7-a8697f0eab0a">

   ### Implementations:
   1. *HashSet:* Implementation done by array of LinkedList + Hashing
   2. *LinkedHashSet*
   3. *TreeSet*

------

### 3. Queue:
   * It is an Interface.
   * By default FIFO. But order can be changed by priority.
   * Insertion happens on one end and deletion happens on the other.
   * In Dequeue, we can insert and delete from any of the ends.
   * Queue is not thread safe.
   * UseCase: Chat, Messaging Service, Email

   <img width="999" alt="Screenshot 2024-06-27 at 9 35 34 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d1bfd0ee-5910-4d66-96bc-b0ab42fcc915">
   <img width="1020" alt="Screenshot 2024-06-27 at 9 35 41 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/4996efd9-b71b-4589-8eb3-03100be723ab">

   ------
   ### Implementation Class: *PriorityQueue* (also knows as minHeap/maxheap)

   *PriorityQueue* doesn't follow FIFO by default. It follows Natural Order.

   ------
  
   Let's observe,

   <img width="675" alt="Screenshot 2024-06-27 at 9 19 18 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9085ea4e-1ebe-4bfe-8689-8c941d7fba87">

   Elements are removed as per natural order.

   <img width="522" alt="Screenshot 2024-06-27 at 9 20 05 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/14410bb7-e62f-42f4-812d-0e4d85710805">

   ------
   ### Note:
   It can be changed using Comparable & Comparator. We can give our own order.

   ------

   <img width="958" alt="Screenshot 2024-06-27 at 9 36 34 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/025a67a5-2d4e-4920-8dee-93530626beeb">

   There a Collections Class which is part of Collections framework which contains some commonly used methods eg. Collections.sort.

   For Natural ordering, we can implement an interface called *Comparable*. There's a method called *compareTo* where we can provide rules     of Natural ordering.

   For *Custom sorting order*, we can use *Comparator*. We can implement Comparator and override a method called *compare* and put custom      compare logic.

### 4. Map:
   * This has key-value pair.
   * These are not Synchronized/Thread safe.

   <img width="1010" alt="Screenshot 2024-06-27 at 9 36 16 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/3012594f-e56b-48d8-b30e-18383bbf49cb">

   ### Implementations:

   1. *HashMap:* No ordering
   2. *LinkedHashMap:* Insertion order
   3. *Treemap:* Sorted order of keys

   ------
   ### Note:
   
   * *HashMap:* Not Thread safe.
   * *HashTable:* Thread safe. Only one gets to access a block. This makes it time consuming. It locks everything completely.
     Nothing will be accessible.
   * *ConcurrentHashMap:* Thread safe. This allows Concurrent access. It divides complete HashMap into multiple Buckets.
     - Analogy: If data of a person lies in a particular Bucket, only that person gets access. However, others don't get blocked. They get         access to other Buckets.
  ------

   <img width="1010" alt="Screenshot 2024-06-27 at 9 36 22 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/bd02a2fe-8eaa-42a8-81ac-0346877e24f0">
   <img width="979" alt="Screenshot 2024-06-27 at 9 36 29 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2dfedd19-c974-495e-af10-7e994d87d2ef">
   
### Questions

##### 1. Why Indexes Started from zero?
##### 2. "Parent interface can refer to the child". Which principle is this?
   - Polymorphism
##### 3. Are Maps part of Collections framework?
   - Yes. Map interface is a part of Java Collection Framework, but it doesn't inherit Collection Interface. 





