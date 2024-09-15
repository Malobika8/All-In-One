# Pass by Value VS Pass by Reference

### Java is always pass by value

The terms "pass-by-value" and "pass-by-reference" have special, precisely defined meanings in computer science. These meanings differ from 
the intuition many people have when first hearing the terms. Much of the confusion in this discussion seems to come from this fact.

The terms "pass-by-value" and "pass-by-reference" are talking about variables. Pass-by-value means that the value of a variable is passed 
to a function/method. Pass-by-reference means that a reference to that variable is passed to the function. The latter gives the function a 
way to change the contents of the variable.

By those definitions, Java is always pass-by-value. Unfortunately, when we deal with variables holding objects we are really dealing with 
object-handles called references which are passed-by-value as well. 

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


