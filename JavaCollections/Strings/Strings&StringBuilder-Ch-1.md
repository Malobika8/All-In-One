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

### String Comparisons

- Comparator ( == ) : This checks both the values/content and reference variables (if they are pointing to the same object).

  <img width="1001" alt="Screenshot 2024-06-26 at 3 01 30 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/0a006f93-08f4-4e56-91f3-86e1ed80d5a2">

- equals : This checks only the values/content of the object referenced.

### How to create dfferent objects with same content(or value)?

We can create object using "New" keyword. These objects will be created outside the Pool but in heap.

<img width="1002" alt="Screenshot 2024-06-26 at 3 03 56 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7d736284-60e3-4556-8681-baccf35ca4c9">

In this case, if we do "a == b", it will return false because although the content of the object is same, objects are different.

**Note:** *println* always prints a String. It calls the valueOf method which furthur calls toString method.

### Pretty Printing

<img width="723" alt="Screenshot 2024-06-26 at 6 15 33 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2ed7488f-a06b-419b-b4e7-6448e65aa784">
<img width="400" alt="Screenshot 2024-06-26 at 6 15 38 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/11eccfaf-4fdd-435a-8603-99c36dabd078">
<img width="651" alt="Screenshot 2024-06-26 at 6 17 03 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/29ee1d55-2306-431a-ac7b-929eac30a327">
<img width="427" alt="Screenshot 2024-06-26 at 6 17 07 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8b573e5c-5e8a-42c2-999b-a636f6b5a9fd">
<img width="802" alt="Screenshot 2024-06-26 at 6 17 38 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/1ebcb251-324c-4c46-8242-1f6669e5956f">
<img width="412" alt="Screenshot 2024-06-26 at 6 17 49 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/fd8a3af8-d55d-4f40-904f-f5292cedb715">
<img width="690" alt="Screenshot 2024-06-26 at 6 18 56 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/467d56a9-acf0-48f2-b048-130026c55610">

### Operators (+)

Objects are converted to Strings and then concatenated. Operators are only defined for primitives/objects & when one of the values is a String. Atleast one of the items need to be a String & the entire result will be of String type.

int will be converted to Integer that will call toString(). This will be same as "a"+"1".

<img width="789" alt="Screenshot 2024-06-26 at 6 34 40 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/82104018-9236-407f-811b-fb7f40244adc">
<img width="763" alt="Screenshot 2024-06-26 at 6 34 55 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/34b4c5d2-020e-4fc2-a326-9ed77fed4365">

<img width="1019" alt="Screenshot 2024-06-26 at 6 36 27 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/dc567b49-77f6-419e-ab27-7e0c93cf21c3">

### Performance

Consider this piece of code,

<img width="854" alt="Screenshot 2024-06-26 at 6 42 12 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ca3bbefa-c49f-471c-a373-e1df2f2b0904">

Let's try to analyze some problems associated.

There will be a lot of memory wastage as referenced variable will be pointing to the new object in every iteration.

<img width="1006" alt="Screenshot 2024-06-26 at 3 06 16 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/1cdb9373-a3e0-4afa-9e97-5c3071e43d8d">
<img width="1017" alt="Screenshot 2024-06-26 at 6 46 21 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c03701e1-b3c4-4ef7-9ae0-2b7829618831">

It would have been better if there was a DataType/Class which could allow us to modify the value since String doesn't allow us to modify.

For eg, if we make changes to an object, it should change the existing object rather than dumping the same and creating a new one.

### StringBuilder

Only one object is created and changes are made to that object only.

StringBuilder is a class in the Java API that provides a mutable sequence of characters. It is used for dynamic string manipulation, such as building strings from many smaller strings or appending new characters to an existing string. It is similar to the String class, but it is designed for use as a drop-in replacement for StringBuffer in places where the string buffer was being used by a single thread (as it is not synchronized). StringBuilder is more efficient than StringBuffer because it is not synchronized, making it suitable for use in multithreaded environments. It is commonly used for building strings incrementally, such as when parsing a large amount of text or generating a string dynamically.

<img width="827" alt="Screenshot 2024-06-26 at 6 52 51 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/75bfa3a3-b458-420f-a342-caabab074f70">

Similar to String, there are multiple methods available that can be used as well as per requirement.

#### Q. Check if a String is palindrome.

Take two pointers, one at the start and one at the end. 

```
if (start==end)
  move start by 1;
  reduce end by 1;

continue checking till (start>end) OR if at any point of time (start!=end)
```

<img width="1017" alt="Screenshot 2024-06-26 at 6 47 10 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/cf83f2ac-c786-4417-b643-881e8ce53f70">
<img width="1013" alt="Screenshot 2024-06-26 at 6 47 16 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b75d6f75-4cac-4844-b3fe-58ba653bdf77">

## Notes

https://github.com/Malobika8/DSA-Bootcamp-Java/tree/main/lectures/12-strings





















