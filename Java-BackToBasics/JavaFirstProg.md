## How do we convert ".java" file into bytecode ".class file"?

- "javac" (Java Compiler). In JDK, we have Java Compiler.
- To compile, "*javac \<ClassName\>.java*"
- To run, "*java \<Classname\>*"

Let's now look at the following piece of code

<img width="657" alt="Screenshot 2024-06-14 at 11 29 07 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/09220e8d-0e4c-436a-bd74-5d99985ad4a2">

- Public: Access specifier. "Public" can be accessed from anywhere
- Class: Named group of properties and functions
- Main: Name of the file
- main: Keyword. This method is the entry point of a Java program
- static: Object of the class not required to call the method/property
- void: Return type of the method
- String[] args: Collection of Strings
- System.out.println: "out" is a reference variable in "System" class where "out" is of type "PrintStream". "println" is a method available in
  "PrintStream" Class which lets user to print the String

  <img width="657" alt="Screenshot 2024-06-14 at 11 29 07 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/4d94d49c-8131-4786-9b4a-550e81f00fc3">

  out is by default null which basically refers to Standard output. If we want the output to be printed in a File we can do, "*out=\<File\>*"

  "System.out" - Standard Output (Command Line/Terminal)

  <img width="520" alt="Screenshot 2024-06-14 at 1 12 40 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a31995f1-f657-461c-a332-2c2a36f78d9a">

- To change location to store the bytecode, we can use "d" flag: "*javac -d . Demo.java*"
- Package is the folder in which our Java File lies.

## How to input data?

There's "Scanner" class in "java.util" package that can be made use of. While creating the object, we need to mention from where do we want the
data to be inputted. 

* "System.in" - Standard Input (From Keyboard)

  <img width="754" alt="Screenshot 2024-06-14 at 12 45 46 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/747369a0-ec9c-405f-9d1a-493c73d8c8cd">

* Primitives:  In Java programming language, primitive data types are basic data types that are built-in with the language. They include byte,
  short, int, long, float, double, and boolean. These data types are used to represent fundamental units of data in computer memory. They are
  also referred to as value data types, as their value represents the data they contain.

  Primitive data types are used extensively throughout a program, and it is important for programmers to understand their characteristics and
  limitations. Each primitive data type has a specific range of values it can represent, as well as a set of operators that can be used to
  manipulate that type.

  In contrast to primitive data types, non-primitive data types, also known as object.

  <img width="824" alt="Screenshot 2024-06-14 at 1 02 02 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9aefec17-728c-49a3-91fe-1ef7d3b2d1c2">

  By default, all the decimal values that we have are of type decimal. If we want to store them in float, we need to append an "f".
  Similarly, by default, all the integer values are of type int. If we want to store large integers in long, we need to append an "L".

* Input values of different data types:
  - If we want to input byte: "*byte num = input.nextByte();*"
  - If we want to input int: "*int rollNo = input.nextInt();*"
  - If we want to input long: "*long distanceFromSun = input.nextLong();*"
  - If we want to input float: "*float marks = input.nextFloat();*"
  - If we want to input double: "*double percentage = input.nextDouble();*"
  - If we want to input Boolean: "*Boolean flag = input.nextBoolean();*"
  - If we want to input String: "*String name = input.next();*"
  - If we want to input entire line: "*String sentence = input.nextLine();*"
  - If we want to input char: "*char name = input.next().charAt(0);*"


## Q. From where is the computer finding "javac" though?

- "javac" is basically an executable file that is located somewhere in our computer.
- We can check the location using "where javac" command
- Our computer automatically locates the exe through PATH VARIABLE / ENVIRONMENT VARIABLE
- ENVIRONMENT VARIABLE is basically a list of folder address in which our computer checks whether the command that we have written is
  available or not

## Type Conversion - Explicit & Implicit

Exceeds size limit. So it does result%size

<img width="822" alt="Screenshot 2024-06-14 at 1 27 38 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/72cfa60e-52bf-4656-a7f3-798c49c17d70">

## Type promotion rules
- byte,short,char will be promoted to int
- if any one of the operands is long, whole operation will be promoted to long
- if any one of the operands is float, result will be float
- if any one of the operands is double, result will be double

<img width="812" alt="Screenshot 2024-06-14 at 1 38 46 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a75cd55a-40b4-42c2-b0cb-0fc211a15e6e">
<img width="680" alt="Screenshot 2024-06-14 at 1 39 01 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/f28d5413-8c21-4770-98d3-24cf020b66ca">

## Encoding Systems

<img width="1023" alt="Screenshot 2024-08-31 at 10 26 31 PM" src="https://github.com/user-attachments/assets/af16f98d-d6d7-4d66-a35a-554dfdc9962e">

## Unicode

In Java, Unicode refers to the standard for representing characters from different writing systems in a single, uniform way. It allows for the use of a wide range of characters, including those that are not part of the ASCII character set, such as accented letters, symbols, and emojis. Unicode is used in Java through the use of the Unicode Standard, which defines the encoding of characters and provides a way to represent them in different formats. In Java, Unicode is typically used in conjunction with the String class, which represents a sequence of characters in a specific encoding.  

<img width="747" alt="Screenshot 2024-06-14 at 1 33 22 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/92d6a7d3-a5cc-4486-a7d2-c71ec6f37eb3">
<img width="760" alt="Screenshot 2024-06-14 at 1 33 29 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/3a15cf2c-0b89-42bc-8370-2c3e78601ab4">

## Notes

https://github.com/Malobika8/DSA-Bootcamp-Java/tree/main/lectures/05-first-java-program

Please read - https://www.scaler.com/topics/course/java-beginners/
