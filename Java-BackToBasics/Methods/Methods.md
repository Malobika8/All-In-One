## Function Overloading

In Java, Function Overloading refers to the ability to define multiple methods with the same name but different parameter lists. This allows for more flexibility in defining methods that can accept different types or numbers of parameters. Overloading is a powerful feature that can make your code more readable and maintainable. It helps to make it clear which method should be called based on the arguments passed to it. 

The compiler does not consider the return type while differentiating the overloaded method. But you cannot declare two methods with the same signature and different return types. It will throw a compile-time error. If both methods have the same parameter types, but different return types, then it is not possible.
Java can distinguish the methods with different method signatures. i.e. the methods can have the same name but with different parameters list (i.e. the number of the parameters, the order of the parameters, and data types of the parameters) within the same class. 

<img width="824" alt="Screenshot 2024-06-13 at 10 00 42 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/f237096c-8b92-483b-a78c-37007b23a706">
<img width="702" alt="Screenshot 2024-06-13 at 10 00 55 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a40ff6e5-9d81-4ce0-ab73-44099a7f541e">

### Note:
Empty Parameter not allowed while overriding varargs(variable arguments) as it won't be able to decide which one to call.

In Java, there is no particular thing as *Pass By Reference*. In Java, there is only *PassBy Value*.

In memory, variable is stored in Stack and it references the value which is stored in Heap. Hence, the value is also called as Reference Variable.

When we pass a value to a function, a copy of the value of the reference variable is passed. So the argument in the function references the 
same value in Heap.

<img width="650" alt="Screenshot 2024-06-12 at 7 38 16 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9dace9ad-c155-47d3-9d73-8a6e2710cd24">
<img width="529" alt="Screenshot 2024-06-12 at 7 38 19 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/34ada3bf-e90e-4c6b-9f23-ca4b2a409490">

# Variable Arguments

 In Java, variable arguments allow a method to accept a variable number of arguments of the same type or different types. This feature is denoted by the use of the "varargs" keyword in the method signature. For example, a method with varargs can be used to calculate the sum of any number of integers passed to it as arguments, or to concatenate any number of strings. Varargs are typically used in situations where the number of arguments that can be passed to a method is not known in advance or when the method needs to be able to accept any number of arguments of the same or different types.  

It internally stores as array.

<img width="836" alt="Screenshot 2024-06-13 at 9 13 14 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b7faa775-1490-41e4-a919-67df17c41058">
<img width="663" alt="Screenshot 2024-06-13 at 9 13 24 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/84166a1d-8931-48da-ae19-2ac306ce4ffc">

#### But what if we want a mix of arguments?

<img width="842" alt="Screenshot 2024-06-13 at 9 16 03 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/628d77d7-99e7-467e-b3c8-3ec6e396f746">

### Note:
Variable Argument parameter must be last in the list

### Notes

https://github.com/kunal-kushwaha/DSA-Bootcamp-Java/tree/main/lectures/07-methods
