## What are Strings?

A Java string is a sequence of characters that exists as an object of the class java. lang. Java strings are created and manipulated through 
the string class. Once created, a string is immutable -- its value cannot be changed.

Note: primitives are stored in Stack memory.

<img width="805" alt="Screenshot 2024-06-26 at 2 40 37 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/99b09e7c-3cd7-4188-b3a0-50343e050b5f">
<img width="990" alt="Screenshot 2024-06-26 at 2 45 16 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/604706cc-0d4e-425c-b461-8901b4586f00">
<img width="959" alt="Screenshot 2024-06-26 at 2 45 24 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d8653c3f-ef84-4f0e-bb7a-2c2d9f2eb33d">

String Pool is a separate memory structure inside Heap.

<img width="1000" alt="Screenshot 2024-06-26 at 2 45 33 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/fb36d3f8-a56c-40d0-956a-2d530a13df53">

#### But why do we need a separate pool in heap?

All the similar values of Strings are not recreated in the Pool. Heaps makes the program more optimized.

#### Won't change in one reference variable change the other if there are 2 reference variable pointing to the same object?

No it won't as Strings are immutable.



