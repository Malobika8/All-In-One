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

Please read - https://www.scaler.com/topics/java/how-java-program-works/
https://www.geeksforgeeks.org/differences-jdk-jre-jvm/

-------------------------------------------------------------------------------------------------------------------------

## JDK

- Provides javac(compiler - converts source code to bytecode)
- Provides Javadoc
- Provides debugger
- Provides JRE

## JRE

- Provides an environment to run the code
- Provides JVM
- Provides libraries and core classes

## JDK

- Interpreter

# Classloader

Yes, the **ClassLoader** in Java is responsible for loading `.class` files into memory so they can be executed by the Java Virtual Machine (JVM). Here's a breakdown of how this process works:

### 1. **What is a ClassLoader?**
A **ClassLoader** is a part of the Java runtime that is responsible for dynamically loading Java classes into memory when they are needed. It is an integral part of the JVM, ensuring that classes are loaded into memory from sources such as:
- **Local file systems** (e.g., `.class` files on disk)
- **Network sources**
- **JAR files**

### 2. **How Does the ClassLoader Work?**
The general steps involved in the **class loading process** are as follows:

#### Step 1: **Find the Class File**
When a class is referenced for the first time (either through method calls, object instantiation, or field access), the **ClassLoader** tries to locate its corresponding `.class` file. The class file is typically located based on:
- **Classpath**: The classpath is a list of directories, JAR files, or ZIP files where the JVM looks for classes.

#### Step 2: **Load the Class**
Once the `.class` file is found, the **ClassLoader** loads it into the JVM’s memory. This process is handled by reading the binary data of the `.class` file, which contains bytecode that can be executed by the JVM.

#### Step 3: **Verify the Class**
The JVM verifies that the class's bytecode adheres to the correct format and is safe to execute. This ensures that the class doesn't contain malicious code or violate Java's security model.

#### Step 4: **Linking**
Once the class is loaded, it undergoes **linking**, which includes:
- **Verification**: Ensure that the bytecode does not contain invalid code.
- **Preparation**: Allocate memory for static variables and constants.
- **Resolution**: Replace symbolic references in the class (e.g., to other classes or methods) with direct references.

#### Step 5: **Initialize the Class**
If the class contains any **static initializers** (like static blocks or static variables), the **ClassLoader** invokes them when the class is initialized. This is done only once during the lifetime of the class.

#### Step 6: **Execute the Code**
Once the class is loaded, linked, and initialized, the JVM can execute its methods, such as starting a `main` method or invoking a class's functions.

### 3. **Types of Class Loaders**
There are several types of **ClassLoaders** in Java:

- **Bootstrap ClassLoader**: Loads core Java classes (like `java.lang.*`).
- **Extension ClassLoader**: Loads classes from the Java extensions directory (`$JAVA_HOME/lib/ext`).
- **System/Application ClassLoader**: Loads classes from the directories or JAR files specified in the classpath.

In addition, you can also create custom **ClassLoaders** for loading classes from non-standard locations, like a database or network.

---

### Example:
When you run a Java program, like:
```java
public class MyClass {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

Here’s how the **ClassLoader** works:
1. The JVM starts by using the **Bootstrap ClassLoader** to load the core classes like `java.lang.String` and `java.lang.System`.
2. The **System ClassLoader** (or **Application ClassLoader**) loads `MyClass` from the classpath.
3. The JVM reads the bytecode from `MyClass.class` and loads it into memory.
4. The class is verified, linked, and initialized.
5. The `main` method of `MyClass` is executed.

---

### Summary:
The **ClassLoader** in Java is responsible for dynamically loading classes (e.g., `.class` files) into memory. It finds, loads, verifies, links, and initializes classes before they can be used by the JVM. The class loading process ensures that Java classes are safely and efficiently loaded into memory for execution.

# JVM - OS dependent

The **Java Virtual Machine (JVM)** is **OS-dependent**. Here's why and how it works:

### Why is the JVM OS-dependent?
The JVM serves as an abstraction layer between the Java bytecode (which is platform-independent) and the underlying operating system. While the **Java bytecode** is platform-independent, the **JVM implementation** must interact with the underlying hardware and operating system to perform tasks like:

- Memory management
- File I/O
- Network communication
- Thread scheduling

Each operating system (e.g., Windows, macOS, Linux) has its own architecture and system calls, so the JVM must be tailored to work with the specifics of that OS.

### Key Points:
1. **JVM is OS-dependent**:
   - Different operating systems require different JVM implementations.
   - For example:
     - On Windows, you might have `java.exe` as the JVM binary.
     - On Linux, you might have `java` as the JVM binary.

2. **Java is platform-independent**:
   - The bytecode generated by `javac` can run on any machine with a compatible JVM, regardless of the operating system.
   - This is why Java has the "write once, run anywhere" capability.

3. **Different JVM implementations**:
   - Oracle JVM
   - OpenJDK JVM
   - IBM JVM
   - These implementations may vary in performance but still adhere to the Java Virtual Machine Specification.

---

### Summary
- The **JVM** is **OS-dependent** because it interacts directly with the operating system.
- However, Java bytecode remains **platform-independent**, and any OS-specific JVM can execute it.

# Leetcode and other platforms

Yes, platforms like **LeetCode**, **HackerRank**, and **Codeforces** use different interpreters or virtual machines to execute code for each supported programming language. Here's how it works:

---

### How Platforms Like LeetCode Run Code

1. **Java (JVM)**:
   - For Java submissions, platforms use the **Java Virtual Machine (JVM)** to compile (`javac`) and run (`java`) the code.
   - The JVM handles bytecode execution, making Java code platform-independent.

2. **Python (CPython)**:
   - For Python submissions, they typically use the **CPython interpreter**, the most common implementation of Python.
   - The source code is compiled into Python bytecode, which is then executed by the Python Virtual Machine (PVM).

3. **C/C++ (GCC or Clang)**:
   - C/C++ code is compiled using compilers like **GCC** (GNU Compiler Collection) or **Clang**.
   - The resulting machine code is executed directly by the underlying hardware, leading to very fast performance.

4. **JavaScript (Node.js or V8)**:
   - JavaScript submissions often use **Node.js** or the **V8 JavaScript engine** (used in Chrome) to execute the code.
   - These engines interpret and execute JavaScript efficiently.

5. **Other Languages**:
   - Platforms provide specific compilers or interpreters for other languages, such as:
     - **Ruby**: MRI (Matz's Ruby Interpreter)
     - **Go**: Native Go compiler (`go run`)
     - **Kotlin**: Kotlin's JVM or native compiler

---

### Why Different Interpreters and Runtimes?
- **Language-Specific Requirements**: Each language has its own syntax, semantics, and runtime behavior.
- **Optimized Execution**: Using the native interpreter or virtual machine ensures optimal performance and correct execution of language features.
- **Isolation and Security**: Code is typically executed in isolated environments (e.g., Docker containers) to prevent interference between user submissions.

---

### Execution Workflow on Platforms:
1. User submits code.
2. The platform sends the code to a language-specific **interpreter, compiler, or virtual machine**.
3. The compiled or interpreted code runs in a sandboxed environment.
4. Outputs (e.g., results, errors, or runtime) are captured and displayed to the user.

---

### Summary
Yes, platforms like LeetCode use different interpreters or runtimes depending on the programming language, such as the **JVM for Java**, **CPython for Python**, and **Node.js for JavaScript**, to ensure language-specific behavior and performance.
