# Pass by Value VS Pass by Reference

### Java is always pass by value

The terms "pass-by-value" and "pass-by-reference" have special, precisely defined meanings in computer science. These meanings differ from 
the intuition many people have when first hearing the terms. Much of the confusion in this discussion seems to come from this fact.

The terms "pass-by-value" and "pass-by-reference" are talking about variables. Pass-by-value means that the value of a variable is passed 
to a function/method. Pass-by-reference means that a reference to that variable is passed to the function. The latter gives the function a 
way to change the contents of the variable.

By those definitions, Java is always pass-by-value. Unfortunately, when we deal with variables holding objects we are really dealing with 
object-handles called references which are passed-by-value as well. 

In Java, the method of passing arguments to methods is **pass-by-value**. However, this can be a bit confusing because **objects** and **primitive types** are passed in different ways.

### 1. **Primitive Types (e.g., `int`, `char`, `float`)**:
When you pass a **primitive type** to a method, Java passes the **value** of the variable (a copy of the value). This means that changes made to the parameter inside the method do not affect the original value.

#### Example:
```java
public class PassByValue {
    public static void main(String[] args) {
        int x = 10;
        modify(x);
        System.out.println(x); // Outputs 10 (no change)
    }

    public static void modify(int a) {
        a = 20; // Modifies only the local copy of 'a'
    }
}
```
- In this case, `x` is passed by value, so the method `modify` only changes the copy of `x`, not the original variable.

### 2. **Objects (e.g., arrays, custom classes)**:
When you pass an **object** to a method, you are passing the **reference** (the memory address) to that object, **but** the reference itself is passed by value. This means the method gets a copy of the reference to the object. While the object itself can be modified (since both the original and the copy of the reference point to the same object), the reference cannot be changed to point to a different object.

#### Example:
```java
public class PassByReference {
    public static void main(String[] args) {
        Person p = new Person("Alice");
        modify(p);
        System.out.println(p.name); // Outputs "Bob" (changed inside modify)
    }

    public static void modify(Person person) {
        person.name = "Bob"; // Changes the object that 'person' points to
    }
}

class Person {
    String name;
    Person(String name) {
        this.name = name;
    }
}
```
- In this case, the **reference to the `Person` object** is passed by value. The object inside the method is modified, so the changes are reflected outside the method, because both the original and the copied reference point to the same object.

#### What Happens with Object References:
- The reference itself is passed **by value**: you can't change the reference to point to a new object.
- The object that the reference points to can be **modified** inside the method.

### Key Takeaways:
- **Java is always pass-by-value**. 
- For **primitive types**, the value itself is passed.
- For **objects**, the reference (memory address) to the object is passed by value. This allows the method to modify the object, but not the reference itself.


## Watch this
https://www.youtube.com/watch?v=-5NC5_sI-vQ

# What is Polymorphism in Java?
Polymorphism is considered one of the important features of Object-Oriented Programming. Polymorphism allows us to perform a single action 
in different ways. In other words, polymorphism allows you to define one interface and have multiple implementations. The word “poly” means 
many and “morphs” means forms, So it means many forms.

## Types of Java Polymorphism
In Java Polymorphism is mainly divided into two types: 

- ### Compile-time Polymorphism:

  It is also known as static polymorphism. This type of polymorphism is achieved by function overloading. When
  there are multiple functions with the same name but different parameters then these functions are said to be overloaded. Functions can be
  overloaded by changes in the number of arguments or/and a change in the type of arguments.

  #### Note
    A method signature is a combination of a method's name and its parameters, which is used to identify a method in object-oriented programming: 
    - Method name: A unique identifier for the method 
    - Parameters: The input to the method, which includes the number, type, and order of the parameters
  
- ### Runtime Polymorphism (Dynamic Method Dispatch):

  It is also known as Dynamic Method Dispatch. It is a process in which a function call to the overridden method is resolved at Runtime.
  This type of polymorphism is achieved by Method Overriding. Method overriding, on the other hand, occurs when a derived class has a
  definition for one of the member functions of the base class. That base function is said to be overridden.


