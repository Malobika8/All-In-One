## Principles

1. Inheritance:

   Inheritance is an important pillar of OOP(Object-Oriented Programming). It is the mechanism in Java by which one class is allowed to         inherit the features(fields and methods) of another class. In Java, Inheritance means creating new classes based on existing ones. A         class that inherits from another class can reuse the methods and fields of that class. In addition, you can add new fields and methods to    your current class as well.  

   ### Why Do We Need Java Inheritance?
   - Code Reusability: The code written in the Superclass is common to all subclasses. Child classes can directly use the parent class code.
   - Method Overriding: Method Overriding is achievable only through Inheritance. It is one of the ways by which Java achieves Run Time           Polymorphism.
   - Abstraction: The concept of abstract where we do not have to provide all details, is achieved through inheritance. Abstraction only          shows the functionality to the user.

   FYI:
   - Every class inherits *Object* class
   - We can access properties of the super class using "super" keyword. E.g.: super.weight;

2. Polymorphism:

   The word polymorphism means having many forms. In simple words, we can define Java Polymorphism as the ability of a message to be            displayed in more than one form.

   Real-life Illustration of Polymorphism in Java: A person at the same time can have different characteristics. Like a man at the same time    is a father, a husband, and an employee. So the same person possesses different behaviors in different situations. This is called            polymorphism. 

   ### What is Polymorphism in Java?
   Polymorphism is considered one of the important features of Object-Oriented Programming. Polymorphism allows us to perform a single          action in different ways. In other words, polymorphism allows you to define one interface and have multiple implementations. The word        “poly” means many and “morphs” means forms, So it means many forms.

   ### Types of Java Polymorphism
   In Java Polymorphism is mainly divided into two types: 

   - Compile-Time Polymorphism in Java: (Which method to be called is determined at compile-time)

     It is also known as static polymorphism. This type of polymorphism is achieved by function overloading or operator overloading. 

     Note: But Java doesn’t support the Operator Overloading.

     ### Method Overloading (Same name but different parameters, order, or return type)

     When there are multiple functions with the same name but different parameters then these functions are said to be overloaded. Functions      can be overloaded by changes in the number of arguments or/and a change in the type of arguments.

   - Runtime Polymorphism in Java:
     
     It is also known as Dynamic Method Dispatch. It is a process in which a function call to the overridden method is resolved at Runtime.       This type of polymorphism is achieved by Method Overriding. Method overriding, on the other hand, occurs when a derived class has a          definition for one of the member functions of the base class. That base function is said to be overridden.

     <img width="1125" alt="Screenshot 2024-07-16 at 7 32 37 PM" src="https://github.com/user-attachments/assets/61a9835a-3252-423d-9193-46cc7bcb0e95">

     ### How Java determines which one to all?

     Dynamic Method Dispatch - Mechanism that determines at runtime which version of the method to call based on the type of the Object.

     
