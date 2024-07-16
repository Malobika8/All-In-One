# Access Modifiers in Java

in Java, Access modifiers help to restrict the scope of a class, constructor, variable, method, or data member. It provides security, accessibility, etc to the user depending upon the access modifier used with the element. Let us learn about Java Access Modifiers, their types, and the uses of access modifiers in this article.

## Types of Access Modifiers in Java
There are four types of access modifiers available in Java: 

- Default – No keyword required
- Private
- Protected
- Public

<img width="1153" alt="Screenshot 2024-07-16 at 8 14 32 PM" src="https://github.com/user-attachments/assets/3021111b-878f-43b3-bc6a-69fae46c4d9e">

## Java Access Modifiers
### Default Access Modifier
When no access modifier is specified for a class, method, or data member – It is said to have the default access modifier by default. The data members, classes, or methods that are not declared using any access modifiers i.e. having default access modifiers are accessible only within the same package.

In this example, we will create two packages and the classes in the packages will have the default access modifiers and we will try to access a class from one package from a class of the second package.

Program 1:

```
// Java program to illustrate default modifier 
package p1; 

// Class Geek is having Default access modifier 
class Geek 
{ 
    void display() 
    { 
        System.out.println("Hello World!"); 
    } 
}
```

Program 2:

```
// Java program to illustrate error while 
// using class from different package with 
// default modifier 
package p2; 
import p1.*; 

// This class is having default access modifier 
class GeekNew 
{ 
    public static void main(String args[]) 
    { 
        // Accessing class Geek from package p1 
        Geek obj = new Geek(); 

        obj.display(); 
    } 
}
```

#### Output:

Compile time error

### Private Access Modifier:
   
The private access modifier is specified using the keyword private. The methods or data members declared as private are accessible only within the class in which they are declared.

Any other class of the same package will not be able to access these members.
Top-level classes or interfaces can not be declared as private because private means “only visible within the enclosing class”.
protected means “only visible within the enclosing class and any subclasses”
Hence these modifiers in terms of application to classes, apply only to nested classes and not on top-level classes

In this example, we will create two classes A and B within the same package p1. We will declare a method in class A as private and try to access this method from class B and see the result.

```
// Java program to illustrate error while
// Using class from different package with

// Private Modifier
package p1;

// Class A
class A {
    private void display()
    {
        System.out.println("GeeksforGeeks");
    }
}

// Class B
class B {
    public static void main(String args[])
    {
        A obj = new A();
        // Trying to access private method
        // of another class
        obj.display();
    }
}
```

#### Output:

error: display() has private access in A
        obj.display();

### Protected Access Modifier:
   
The protected access modifier is specified using the keyword protected.

The methods or data members declared as protected are accessible within the same package or subclasses in different packages.

In this example, we will create two packages p1 and p2. Class A in p1 is made public, to access it in p2. The method display in class A is protected and class B is inherited from class A and this protected method is then accessed by creating an object of class B.

Program 1:

```
// Java Program to Illustrate
// Protected Modifier
package p1;

// Class A
public class A {
    protected void display()
    {
        System.out.println("GeeksforGeeks");
    }
}
```

Program 2:

```
// Java program to illustrate
// protected modifier
package p2;

// importing all classes in package p1
import p1.*; 

// Class B is subclass of A
class B extends A {
    public static void main(String args[])
    {
        B obj = new B();
        obj.display();
    }
}
```

#### Output:

GeeksforGeeks

### Public Access modifier:
   
The public access modifier is specified using the keyword public. 

The public access modifier has the widest scope among all other access modifiers.
Classes, methods, or data members that are declared as public are accessible from everywhere in the program. There is no restriction on the scope of public data members.

Program 1:

```
// Java program to illustrate 
// public modifier 
package p1; 
public class A 
{ 
public void display() 
    { 
        System.out.println("GeeksforGeeks"); 
    } 
}
```

Program 2:

```
package p2;
import p1.*;
class B {
    public static void main(String args[])
    {
        A obj = new A();
        obj.display();
    }
}
```

#### Output:

GeeksforGeeks

###  Important Points:

If other programmers use your class, try to use the most restrictive access level that makes sense for a particular member. Use private unless you have a good reason not to.
Avoid public fields except for constants.

### Algorithm to use access modifier in Java
Here’s a basic algorithm for using access modifiers in Java:

- Define a class: Create a class that represents the object you want to manage.
- Define instance variables: Within the class, define instance variables that represent the data you want to manage.
- Specify an access modifier: For each instance variable, specify an access modifier that determines the visibility of the variable. The three main access modifiers in Java are private, protected, and public.
- Use private for variables that should only be accessible within the class: If you want to prevent access to a variable from outside the class, use the private access modifier. This is the most restrictive access modifier and provides the greatest level of encapsulation.
- Use protected for variables that should be accessible within the class and its subclasses: If you want to allow access to a variable from within the class and its subclasses, use the protected access modifier. This is less restrictive than private and provides some level of inheritance.
- Use public for variables that should be accessible from anywhere: If you want to allow access to a variable from anywhere, use the public access modifier. This is the least restrictive access modifier and provides the least amount of encapsulation.
- Use accessor and mutator methods to manage access to the variables: In order to access and modify the variables, use accessor (getter) and mutator (setter) methods, even if the variables have a public access modifier. This provides a level of abstraction and makes your code more maintainable and testable.

## FAQs in Access Modifiers

1. What are access modifiers in Java?
   
- Access modifiers in Java are the keywords that are used for controlling the use of the methods, constructors, fields, and methods in a class.

2. What is void in Java?
   
- Void in Java is used to specify no return value with the method.

3. What are the 12 modifiers in Java?
   
- 12 Modifiers in Java are public, private, protected, default, final, synchronized, abstract, native, strictfp, transient, and volatile.

# Packages

- User defined
- In-built:
  - lang: Java language specific stuff. (implicitly imported)

    Every compilation unit implicitly imports every public type name declared in the predefined package java. lang , as if the declaration
    "import java. lang. *;" appeared at the beginning of each compilation unit immediately after any package declaration.

    ```
     In Java, all classes and interfaces are implicitly imported from the `java.lang` package. This means that you don't need to explicitly
     import classes like `String`, `System`, `Integer`, and others from `java.lang` to use them in your code. This is because `java.lang` is
     automatically imported by the Java compiler, allowing you to access its classes and members without additional import statements.
     This helps simplify your code and reduces the amount of boilerplate imports.
    ```
    
  - io: Input Output related items.
  - util: Utility classes.
  - applet: More on the development side.
  - awt
  - net


## FYI
* Hashcode: Random number generated to differentiate different objects.
* To check if an object is an instance of a Class: use "instanceOf()" method.
* To get any info related to a Class: use "getClass()" method.

*Note: Check Object class*


