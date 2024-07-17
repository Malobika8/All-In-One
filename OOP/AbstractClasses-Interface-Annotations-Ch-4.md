# Abstract Method in Java

In Java, Sometimes we require just method declaration in super-classes. This can be achieved by specifying the Java abstract type modifier. 
Abstraction can be achieved using abstract class and abstract methods.

The abstract Method is used for creating blueprints for classes or interfaces. Here methods are defined but these methods don’t provide the 
implementation. Abstract Methods can only be implemented using subclasses or classes that implement the interfaces.

These methods are sometimes referred to as subclass responsibility because they have no implementation specified in the super-class. Thus, a 
subclass must override them to provide a method definition. 

### Declare Abstract Method in Java
To declare an abstract method, use this general form:
```
abstract type method-name(parameter-list);
```

As you can see, no method body is present. Any concrete class(i.e. class without abstract keyword) that extends an abstract class must 
override all the abstract methods of the class.

<img width="894" alt="Screenshot 2024-07-17 at 2 14 54 PM" src="https://github.com/user-attachments/assets/331fa4da-097e-4702-b15a-7ad6c2168b88">
<img width="889" alt="Screenshot 2024-07-17 at 2 15 44 PM" src="https://github.com/user-attachments/assets/2a22e949-af8c-4347-832f-c06875b05208">
<img width="882" alt="Screenshot 2024-07-17 at 2 15 54 PM" src="https://github.com/user-attachments/assets/64938baf-ce96-4114-a0fa-7e36fdb6c208">

### Important rules for abstract methods are mentioned below:

- Any class that contains one or more abstract methods must also be declared abstract.
- If a class contains an abstract method it needs to be abstract and vice versa is not true.
- If a non-abstract class extends an abstract class, then the class must implement all the abstract methods of the abstract class else the concrete class has to be declared as abstract as well.
- Abstract classes can have constructors but Object of abstract classes cannot be created.
- Abstract classes can have concrete classes.
- The following are various illegal combinations of other modifiers for methods with respect to abstract modifiers: 
  - final
  - abstract native
  - abstract synchronized
  - abstract static
  - abstract private
  - abstract strictfp

### Note
```
Although abstract classes cannot be used to instantiate objects, they can be used to create object references, because Java’s approach
to run-time polymorphism is implemented through the use of super-class references. Thus, it must be possible to create a reference to an
abstract class so that it can be used to point to a subclass object.
```

### Java Abstract Method in Interface
All the methods of an interface are public abstract by default because of which we can declare abstract methods inside an interface.

### Final Method in Abstract Class
As we have mentioned that we cannot use final with abstract Method as a modifier but we can create a Final concrete method in abstract class.

# Interfaces in Java
An Interface in Java programming language is defined as an abstract type used to specify the behavior of a class. An interface in Java is a 
blueprint of a behavior. A Java interface contains static constants and abstract methods. By default, the methods are abstract and public in
Interface,

### What are Interfaces in Java?
The interface in Java is a mechanism to achieve abstraction. Traditionally, an interface could only have abstract methods (methods without a
body) and public, static, and final variables by default. It is used to achieve abstraction and multiple inheritances in Java. In other 
words, interfaces primarily define methods that other classes must implement. Java Interface also represents the IS-A relationship.

In Java, the abstract keyword applies only to classes and methods, indicating that they cannot be instantiated directly and must be 
implemented.

When we decide on a type of entity by its behavior and not via attribute we should define it as an interface.

### Features of Interfaces

#### Syntax for Java Interfaces
```
interface {
    // declare constant fields
    // declare methods that abstract 
    // by default.   
}
```

To declare an interface, use the interface keyword. It is used to provide total abstraction. That means all the methods in an interface are 
declared with an empty body and are public and all fields are public, static, and final by default. A class that implements an interface 
must implement all the methods declared in the interface. To implement the interface, use the implements keyword.

### Uses of Interfaces in Java are mentioned below:

- It is used to achieve total abstraction.
- Since java does not support multiple inheritances in the case of class, by using an interface it can achieve multiple inheritances.
- Any class can extend only 1 class, but can any class implement an infinite number of interfaces.
- It is also used to achieve loose coupling.
- Interfaces are used to implement abstraction.
  
### So, the question arises why use interfaces when we have abstract classes?

The reason is, abstract classes may contain non-final variables, whereas variables in the interface are final, public, and static.

```
// A simple interface
interface Player
{
    final int id = 10;
    int move();
}
```

### Relationship Between Class and Interface
A class can extend another class similar to this an interface can extend another interface. But only a class can extend to another interface,
and vice-versa is not allowed.

### Relationship between Class and Interface
#### Difference Between Class and Interface
Although Class and Interface seem the same there have certain differences between Classes and Interface. The major differences between a 
class and an interface are mentioned below:

<img width="710" alt="Screenshot 2024-07-17 at 2 32 42 PM" src="https://github.com/user-attachments/assets/bb1a164f-3500-4f78-93fa-5bdb083e7c16">

#### Implementation: To implement an interface, we use the keyword implements

### Advantages of Interfaces in Java
The advantages of using interfaces in Java are as follows:

- Without bothering about the implementation part, we can achieve the security of the implementation.
- In Java, multiple inheritances are not allowed, however, you can use an interface to make use of it as you can implement more than one interface.

### Multiple Inheritance in Java Using Interface
Multiple Inheritance is an OOPs concept that can’t be implemented in Java using classes. But we can use multiple inheritances in Java using 
Interface. let us check this with an example.

<img width="809" alt="Screenshot 2024-07-17 at 2 33 57 PM" src="https://github.com/user-attachments/assets/51814379-88f0-401a-b08f-d71b4fdccee3">

### New Features Added in Interfaces in JDK 8
There are certain features added to Interfaces in JDK 8 update mentioned below:

1. Prior to JDK 8, the interface could not define the implementation. We can now add default implementation for interface methods. This
   default implementation has a special use and does not affect the intention behind interfaces.
   Suppose we need to add a new function to an existing interface. Obviously, the old code will not work as the classes have not
   implemented those new functions. So with the help of default implementation, we will give a default body for the newly added functions.
   Then the old codes will still work.

   Below is the implementation of the above point:

```
// Java program to show that interfaces can
// have methods from JDK 1.8 onwards

interface In1
{
    final int a = 10;
    default void display()
    {
        System.out.println("hello");
    }
}

// A class that implements the interface.
class TestClass implements In1
{
    // Driver Code
    public static void main (String[] args)
    {
        TestClass t = new TestClass();
        t.display();
    }
}
```

#### Output
hello

2. Another feature that was added in JDK 8 is that we can now define static methods in interfaces that can be called independently without an object. 
   Note: these methods are not inherited.

```
// Java Program to show that interfaces can
// have methods from JDK 1.8 onwards

interface In1
{
    final int a = 10;
    static void display()
    {
        System.out.println("hello");
    }
}

// A class that implements the interface.
class TestClass implements In1
{
    // Driver Code
    public static void main (String[] args)
    {
        In1.display();
    }
}
```

#### Output
hello

### Extending Interfaces
One interface can inherit another by the use of keyword extends. When a class implements an interface that inherits another interface, it 
must provide an implementation for all methods required by the interface inheritance chain.

Program 1:

```
interface A {
    void method1();
    void method2();
}
// B now includes method1 and method2
interface B extends A {
    void method3();
}
// the class must implement all method of A and B.
class gfg implements B {
    public void method1()
    {
        System.out.println("Method 1");
    }
    public void method2()
    {
        System.out.println("Method 2");
    }
    public void method3()
    {
        System.out.println("Method 3");
    }
}
```

Program 2:

```
interface Student  
{
    public void data();
   
}
class avi implements Student
{
    public void data ()
    {
        String name="avinash";
        int rollno=68;
        System.out.println(name);
        System.out.println(rollno);
    }
}
public class inter_face 
{
    public static void main (String args [])
    {
        avi h= new avi();
        h.data();
    }
}
```

#### Output
avinash

In a Simple way, the interface contains multiple abstract methods, so write the implementation in implementation classes. If the 
implementation is unable to provide an implementation of all abstract methods, then declare the implementation class with an abstract 
modifier, and complete the remaining method implementation in the next created child classes. It is possible to declare multiple child 
classes but at final we have completed the implementation of all abstract methods.

In general, the development process is step by step:

Level 1 – interfaces: It contains the service details.
Level 2 – abstract classes: It contains partial implementation.
Level 3 – implementation classes: It contains all implementations.
Level 4 – Final Code / Main Method: It have access of all interfaces data.

Example:

```
// Java Program for
// implementation Level wise
import java.io.*;
import java.lang.*;
import java.util.*;

// Level 1
interface Bank {
    void deposit();
    void withdraw();
    void loan();
    void account();
}

// Level 2
abstract class Dev1 implements Bank {
    public void deposit()
    {
        System.out.println("Your deposit Amount :" + 100);
    }
}

abstract class Dev2 extends Dev1 {
    public void withdraw()
    {
        System.out.println("Your withdraw Amount :" + 50);
    }
}

// Level 3
class Dev3 extends Dev2 {
    public void loan() {}
    public void account() {}
}

// Level 4
class GFG {
    public static void main(String[] args)
    {
        Dev3 d = new Dev3();
        d.account();
        d.loan();
        d.deposit();
        d.withdraw();
    }
}
```

#### Output
Your deposit Amount :100
Your withdraw Amount :50

### New Features Added in Interfaces in JDK 9
From Java 9 onwards, interfaces can contain the following also:

- Static methods
- Private methods
- Private Static methods

### Important Points in Java Interfaces

- We can’t create an instance (interface can’t be instantiated) of the interface but we can make the reference of it that refers to the Object of its implementing class.
- A class can implement more than one interface.
- An interface can extend to another interface or interface (more than one interface).
- A class that implements the interface must implement all the methods in the interface.
- All the methods are public and abstract. And all the fields are public, static, and final.
- It is used to achieve multiple inheritances.
- It is used to achieve loose coupling.
- Inside the Interface not possible to declare instance variables because by default variables are public static final.
- Inside the Interface, constructors are not allowed.
- Inside the interface main method is not allowed.
- Inside the interface, static, final, and private methods declaration are not possible.

## Frequently Asked Questions
1. Can we create abstract Constructors?

   No as we would then need to provide an implementation which would defeat the purpose of abstract.

2. What is a marker or tagged interface?

   Tagged Interfaces are interfaces without any methods they serve as a marker without any capabilities.

3. How many Types of interfaces in Java?

   Types of interfaces in Java are mentioned below:

#### (Functional Interface / Marker interface)

4. Why multiple inheritance is not supported through class in Java?

   Multiple Inheritance is not supported through class in Java so to avoid certain challenges like Ambiguity and diamond problems.

