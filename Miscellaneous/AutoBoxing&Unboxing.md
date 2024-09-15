# AutoBoxing & UnBoxing
In Java, primitive data types are treated differently so there comes the introduction of wrapper classes where two components play a role 
namely Autoboxing and Unboxing. 

# AutoBoxing
Autoboxing refers to the conversion of a primitive value into an object of the corresponding wrapper class 
is called autoboxing. For example, converting int to Integer class. 

The Java compiler applies autoboxing when a primitive value is: 
- Passed as a parameter to a method that expects an object of the corresponding wrapper class.
- Assigned to a variable of the corresponding wrapper class.

### To convert from int to Integer
```
Integer.valueOf(i)
```

### ArrayList AutoBoxing example

Let’s understand how the compiler does autoboxing and unboxing in the example of Collections in Java using generics.

<img width="763" alt="Screenshot 2024-09-15 at 1 36 45 PM" src="https://github.com/user-attachments/assets/d4d33ccc-d9e8-4272-b309-32b4fc1e4385">

What happens implicitly,

<img width="763" alt="Screenshot 2024-09-15 at 1 37 22 PM" src="https://github.com/user-attachments/assets/ba389827-b377-4e7b-b29e-63f891132949">

# UnBoxing
Unboxing on the other hand refers to converting an object of a wrapper type to its corresponding primitive value. 
For example conversion of Integer to int. 

The Java compiler applies to unbox when an object of a wrapper class is: 
- Passed as a parameter to a method that expects a value of the corresponding primitive type.
- Assigned to a variable of the corresponding primitive type.

The following table lists the primitive types and their corresponding wrapper classes, which are used by the Java compiler for autoboxing 
and unboxing.

<img width="844" alt="Screenshot 2024-09-15 at 1 34 27 PM" src="https://github.com/user-attachments/assets/98093503-00bd-427f-a187-8561deba51d9">

### Advantages
- Autoboxing and unboxing lets developers write cleaner code, making it easier to read.
- The technique lets us use primitive types and Wrapper class objects interchangeably and we do not need to perform any typecasting
  explicitly.

### To convert from Integer to int
```
i.intValue()
```
