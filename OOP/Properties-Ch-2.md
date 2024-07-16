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

     ```
     Early Binding (compile-time time polymorphism) As the name indicates, compiler (or linker) directly associate an address to the              function call. It replaces the call with a machine language instruction that tells the mainframe to leap to the address of the function.
     ```

   - Runtime Polymorphism in Java:
     
     It is also known as Dynamic Method Dispatch. It is a process in which a function call to the overridden method is resolved at Runtime.       This type of polymorphism is achieved by Method Overriding. Method overriding, on the other hand, occurs when a derived class has a          definition for one of the member functions of the base class. That base function is said to be overridden.

     <img width="1125" alt="Screenshot 2024-07-16 at 7 32 37 PM" src="https://github.com/user-attachments/assets/61a9835a-3252-423d-9193-46cc7bcb0e95">
  
     ```
     Late Binding : (Run time polymorphism) In this, the compiler adds code that identifies the kind of object at runtime then matches the 
     call with the right function definition
     ```

     ### How Java determines which one to all?

     Dynamic Method Dispatch - Mechanism that determines at runtime which version of the method to call based on the type of the Object.

     **Note: We cannot Override Static methods**

     Overriding depends on Objects but static doesn't depend on objects. hence we cannot Override static methods.

3. Encapsulation: (Done at implementation level)

   Encapsulation in Java refers to integrating data (variables) and code (methods) into a single unit. In encapsulation, a class's variables    are hidden from other classes and can only be accessed by the methods of the class in which they are found.

   ```
   Encapsulation in Java is a fundamental concept of object-oriented programming. It binds together the data and methods that manipulate        that data, and keeps both safe from outside interference and misuse. In Java, encapsulation is achieved through the use of classes and       objects. A class encapsulates the data and methods which operate on that data, providing a controlled interface to the outside world.        This helps to hide the internal implementation details and provides better data security and abstraction. Encapsulation is useful for        reducing errors and making the code more maintainable and flexible.
   ```

4. Abstraction: (Done at design level)

   Abstraction in Java is a fundamental concept that enables you to design classes that hide their implementation details from the outside      world, while exposing only necessary information through public methods. It is a key principle of object-oriented programming (OOP) that     allows you to focus on the essential features of an object rather than its internal workings. In Java, abstraction is achieved through       the use of abstract classes and interfaces, which define a contract that must be implemented by concrete classes.  
     
