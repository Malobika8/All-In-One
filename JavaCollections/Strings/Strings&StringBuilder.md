## What are Strings?

A Java string is a sequence of characters that exists as an object of the class java. lang. Java strings are created and manipulated through 
the string class. Once created, a string is immutable -- its value cannot be changed.

Note: primitives are stored in Stack memory.

<img width="805" alt="Screenshot 2024-06-26 at 2 40 37 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/99b09e7c-3cd7-4188-b3a0-50343e050b5f">
<img width="990" alt="Screenshot 2024-06-26 at 2 45 16 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/604706cc-0d4e-425c-b461-8901b4586f00">
<img width="959" alt="Screenshot 2024-06-26 at 2 45 24 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d8653c3f-ef84-4f0e-bb7a-2c2d9f2eb33d">

String Pool is a separate memory structure inside Heap.

<img width="1000" alt="Screenshot 2024-06-26 at 2 45 33 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/fb36d3f8-a56c-40d0-956a-2d530a13df53">

### But why do we need a separate pool in heap?

All the similar values of Strings are not recreated in the Pool. Heaps makes the program more optimized.

### Won't change in one reference variable change the other if there are 2 reference variable pointing to the same object?

No it won't as Strings are immutable. When we change reference variable, a new object is created.

<img width="836" alt="Screenshot 2024-06-26 at 2 54 17 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/cfc1b98c-c01e-4f4d-83c2-04a464e288d9">
<img width="490" alt="Screenshot 2024-06-26 at 2 54 30 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/183a454b-212f-430c-a2cc-67a13008314f">
<img width="925" alt="Screenshot 2024-06-26 at 2 56 22 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ee9b85f1-c7c9-4fd9-a03e-572b3180508d">

### Why we can't modify String objects?

For security reasons. if content is changed for one reference variable, content for all other reference variable which were pointing to the same would change as well.

<img width="962" alt="Screenshot 2024-06-26 at 3 01 23 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ad2cb6aa-54bc-4a93-8cdb-9d89e0606a40">

### string Comparisons

- Comparator ( == ) : This checks both the values/content and reference variables (if they are pointing to the same object).

  <img width="1001" alt="Screenshot 2024-06-26 at 3 01 30 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/0a006f93-08f4-4e56-91f3-86e1ed80d5a2">

- equals : This checks only the values/content of the object referenced.

### How to create dfferent objects with same content(or value)?

We can create object using "New" keyword. These objects will be created outside the Pool but in heap.

<img width="1002" alt="Screenshot 2024-06-26 at 3 03 56 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7d736284-60e3-4556-8681-baccf35ca4c9">

In this case, if we do "a == b", it will return false because although the content of the object is same, objects are different.

<img width="1002" alt="Screenshot 2024-06-26 at 3 06 07 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/050e5d56-029f-4017-a70b-6293331ac370">








