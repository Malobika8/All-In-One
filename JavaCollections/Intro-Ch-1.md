# Collections Framework

There a Collections Class which is part of Collections framework which contains some commonly used methods eg. Collections.sort.

<img width="1008" alt="Screenshot 2024-06-27 at 8 02 11 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/cbe631c7-e3a2-408a-8d99-a6d0e149041a">

There are multiple concrete classes and interfaces. Collections framework is nothing but implementation of DataStructures.

There exists already implementated classes and interfaces of frequently used Data Structures

<img width="735" alt="Screenshot 2024-06-27 at 7 57 58 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/0c960b3b-505a-4f32-b8d7-6434c6db8d90">
<img width="1022" alt="Screenshot 2024-06-27 at 8 02 17 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/59607c56-bf9c-4a2f-96d1-a1874bb7a26b">

### What did Java provide these? We can impelment these as well
- so that we can forcus on main logic. We just need to know how to use it

Collections is the root interace of the collection hierarchy. It contains common methods for all the collections.
like size, isEmpty, iterator etc.

There are 3 Interfaces:

1. List: It is an ordered collection.
  what is the order followed? It maintains insertion order. its like a sequence
  It has index which helps us access the elements at a particular position and even insert.

  <img width="712" alt="Screenshot 2024-06-27 at 8 35 18 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7d8b0114-f510-4f64-b141-d997526abdfe">

  Under it :
  - ArrayList: Resizeable array implementation of the interface. it can increase its size on the fly. It doubles the size once becomes full.
    Both tha arrays are not maintained. It copies the info from first to second.
    growable but limited. This is more frequesntly used when we have high no of reads. random search is very fast because of cotiguous
    memory allocation.
    
    <img width="744" alt="Screenshot 2024-06-27 at 8 15 01 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a610040d-0e6e-4d43-a210-b62aa2d4c534">
    <img width="694" alt="Screenshot 2024-06-27 at 8 16 26 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/fbacc7b1-3c3a-486e-a469-17727f6e5501">
    <img width="995" alt="Screenshot 2024-06-27 at 8 46 40 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a365b8e4-f08c-42d5-b023-3407d6b9e0d1">

  - LinkedList: Doubly linked list implementation. It is not made of configuous memory allocation. They are connected with each other through pointers
    or references. It maintains insertion order. random access is not fast. We always have to start from the beginning. It we want to insert and delete
    the data agin and again then we want to use linked list. If ararylist if we delete, we have to shift other elements. However, in LL
    we just need to change the references.
 
    <img width="701" alt="Screenshot 2024-06-27 at 8 18 59 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/da17553f-14d7-41b5-bb41-2c771cd6cc69">

    use cases of LL - hashMap, backward and forward button in Chrome use Stack and stack are implemented using LL.
    Q1. Cycle in a LL
    Q2. LRU cache.(Leetcode)

    Note: ArrayList and LL are not synchronized. They are not thread safe.
    LL supports LIFO as well.
    
    <img width="734" alt="Screenshot 2024-06-27 at 8 28 16 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/29ea061c-cb90-4c40-b774-ba6145318542">

    ArrayList & LinkedList overview:

    <img width="997" alt="Screenshot 2024-06-27 at 8 46 46 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ee1456cf-5c21-4ec5-93f5-6fe4d9c72775">

  - Vector: Note: If multiple people try to insert in ArrayZList and LL, there will be lot of issues. That is what happends when multiple threads try to
    access the same block. This is why synchronization is imp so that the data is not corrupted.

    This class is just like ArrayList but along with that it ensures Thread safety. It can be used in a multi-threaded environment and the data
    wont be corrupted.

    This class implements growable array of objects similar to ArrayList.
    This vector is not generally usable. there are better DS that are much faster. This is legacy DS.
    Check this to know more: https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/package-summary.html

    <img width="1002" alt="Screenshot 2024-06-27 at 8 47 32 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d54e2ccd-dacb-4f77-aa74-414b61b85ee5">

  - Stack: This supports LIFO. This is implemented using ArrayList or LL behind the scene.
    Also, Stack extends Vector which means Stacks are also thread safe.

    Stack.push deosn't have synchronized though unlike pop, peek etc. This is because push calls addElement which is synchronized which serves the
    purpose.

    <img width="621" alt="Screenshot 2024-06-27 at 8 36 41 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/de921163-9c02-4646-b64e-916bc66e5918">

2. Set: This need not necessarily to be ordered. By default its not ordered. Its a collection that doesn't contain any duplicate elements.
   This only contains single values.
   
   #### What is the use case of set? What is it best in?
   - This is best in searching. Best case:O(1), worst:O(n)
  
   Hashing is used behind the scenes.
   Lets try to print all the 3 sets

   <img width="651" alt="Screenshot 2024-06-27 at 9 02 06 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/adf52aaf-f7cd-414e-9b78-7e651e446681">
   * first one doesnt follow any order.
   * second one follows insertion order.
   * third one is sorted (searching/insertion O(logn)
   
   <img width="719" alt="Screenshot 2024-06-27 at 9 05 21 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ba937926-5ab9-463e-871a-18a613bd7f27">
   <img width="668" alt="Screenshot 2024-06-27 at 9 10 47 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d20e4a12-2650-4b6e-85e7-a8697f0eab0a">

   3 classes

   - HashSet: Implementation done by array of linkedlist + hashing
  
     
   - LinkedHashSet: 
  
     
   - TreeSet:
  
4. Queue: By default FIFO. But order can be changed by priority. Insertion happens on one end and deletion happens on the other end.
   In Dequeue, we can insert and delete from any of the ends. Queue is not thread safe.

   <img width="999" alt="Screenshot 2024-06-27 at 9 35 34 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d1bfd0ee-5910-4d66-96bc-b0ab42fcc915">
   <img width="1020" alt="Screenshot 2024-06-27 at 9 35 41 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/4996efd9-b71b-4589-8eb3-03100be723ab">

   #### UseCase: Chat is a queue.
   
   It is an Interface.
   The class which implements is ProprityQueues also knows as minHeap/maxheap.
   But PriorityQueue doesnt follow fifo by default. This follows natural order.
  
   Consider the folowing,

   <img width="675" alt="Screenshot 2024-06-27 at 9 19 18 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9085ea4e-1ebe-4bfe-8689-8c941d7fba87">

   Elements are removed as per natural order.

   <img width="522" alt="Screenshot 2024-06-27 at 9 20 05 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/14410bb7-e62f-42f4-812d-0e4d85710805">

   ### We can change this using Comparable & Comparator. We can give our own order.

   <img width="958" alt="Screenshot 2024-06-27 at 9 36 34 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/025a67a5-2d4e-4920-8dee-93530626beeb">

   There a Collections Class which is part of Collections framework which contains some commonly used methods eg. Collections.sort.

   For natural ordering, we can implement an interface called Comparable. There's a method called compareTo where we can give rules of
   natural ordering.

   For custom sorting order, we can use Comparator. We can implement Comparator and override a method called compare and put compare logic.

   ## LL can also follow Queue Interface as it is also doubly ended.

   <img width="580" alt="Screenshot 2024-06-27 at 9 22 50 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7e7d090b-9a0b-47d6-8d09-72093b391315">
   <img width="616" alt="Screenshot 2024-06-27 at 9 22 56 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/5c8670d8-0780-47f0-af78-ebfa6951756a">

   We can use LL as a Queue DS.

6. Map: This has key value pair. These are not synchronized/thread safe.

   <img width="1010" alt="Screenshot 2024-06-27 at 9 36 16 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/3012594f-e56b-48d8-b30e-18383bbf49cb">

   It is made up of 3 things:

   - HashMap: No ordering
   - LinkedHashMap: Insertion order
   - Treemap: Sorted order of keys
  
   There are 3 things:
   - HashMap: Not thread safe.
   - HashTable: Thread safe. Only one will be able to access a block. This makes it time consuming. It locks everything completely.
     Nothing will be accessable.
   - ConcurrentHashMap: Thread safe. This allows concurrent access. It divides complete hashmap into multiple buckets. It a data of that person
     lies in a particular bucket, only that person will get access. But others wont be blocked. They will have access to other buckets.

   <img width="1010" alt="Screenshot 2024-06-27 at 9 36 22 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/bd02a2fe-8eaa-42a8-81ac-0346877e24f0">
   <img width="979" alt="Screenshot 2024-06-27 at 9 36 29 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2dfedd19-c974-495e-af10-7e994d87d2ef">
   
### Questions

##### 1. Why Indexes Started from zero?
##### 2. "Parent interface can refer to the child". Which principle is this?
   - Polymorphism
##### 3. Are Maps part of Collections framework?
   - Maps are part of Collection framework but doesnt implement Collections Class.





