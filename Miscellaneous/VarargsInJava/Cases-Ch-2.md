## Case 1:

#### What if we don't pass any value to method parameter?

- varargs will consider it as an empty array.

<img width="1000" alt="Screenshot 2024-07-06 at 11 11 33 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d4a0cdd1-3089-4eff-901d-c5e63ddd3274">

Run the same,

<img width="1109" alt="Screenshot 2024-07-06 at 11 20 00 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2369b7b2-e8f9-464d-abf2-aac3547b4d41">

## Case 2:

#### What if we overload the method?

- A method which takes varargs as parameter gets the least priority by JVM.

<img width="932" alt="Screenshot 2024-07-06 at 11 16 10 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/673fe56e-f499-4675-9bc9-deaf396fe6ec">
<img width="561" alt="Screenshot 2024-07-06 at 11 16 48 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b74d69c4-9958-45fa-9938-24524d915048">

## Case 3:

#### What if we pass arguments of a type that doesn't match any of the methods?

Consider the following example where *m1()* accepts 3 *int* parameters while the other one accepts *varargs*.

<img width="1121" alt="Screenshot 2024-07-06 at 11 24 50 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d85a0439-9ee1-435d-a112-fcd2b03a0e8b">

In cases when we don't have an exact match, before calling the varargs method directly, JVM checks if there exists any other method which can
handle these values. 

In the example, since **byte** value can be stored inside **int** value, JVM will call the int method (*m1()*).

<img width="1072" alt="Screenshot 2024-07-06 at 11 26 10 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ffbfc891-cb3f-456c-8c16-11a016155af9">

#### What is the reason behind it?

We know that a language needs to be Backward Compatible. Backward Compatibility means the older feature should get more priority than 
newer ones.

Since varargs are defined in 1.5 version compared to normal int parameter method, which is defined in 1.1, older one gets more priority than 
newer one (i.e. varargs).

This makes it Backward Compatible.

## Case 4:

#### Consider the following program and guess the output.

<img width="1065" alt="Screenshot 2024-07-06 at 11 46 26 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d27d0b22-c29b-4ec6-8e85-46b2acd2b3be">

#### Output

<img width="568" alt="Screenshot 2024-07-06 at 11 47 46 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2310eb65-b308-4459-8c95-8d8b5560a1aa">

#### Why this happened?

We cannot pass elements directly to a method that accepts an array. It would have worked if we had passed an array instead of passing elements directly.

Since int can be handled by double, jvm promotes it implicitly and calls the var-args method.

<img width="1144" alt="Screenshot 2024-07-06 at 11 49 50 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/0bec6c5d-06bd-4a5e-8284-81790fbc6f53">





