# Annotations

Annotations are a kind of meta-data. They are supplemental information that we can put into our Java code. They don't directly affect the code 
that we annotate but those annotations can be processed by something else (like a compiler, or at runtime).

Example: @SuppressWarning

<img width="780" alt="Screenshot 2024-07-25 at 10 15 39 PM" src="https://github.com/user-attachments/assets/fc68acd2-7dd1-42f2-a67a-756eab077dd0">

Annotations can be added to anything in Java (Classes, Methods, Variables, Method Parameters, and even other Annotations).

## How do we build our own custom annotations?

Let's say we want to create an annotation that would just apply to a Class. It can be used as a label or signal to some other class processing 
these annotations.

let's try to create an annotation named *@VeryImportant*. Creating an annotation is very similar to creating our own Class. The only change we have to
make to differentiate it from a regular class is to change the keyword "*class*" to "*@interface*"

<img width="867" alt="Screenshot 2024-07-25 at 10 23 08 PM" src="https://github.com/user-attachments/assets/dcce4d72-45df-4954-9f58-b20188a393d4">

Let's try to customize a few things with our annotations before we can actually do something with it. Ironically, to customize annotations, we
need to use some annotations.

There are 2 main annotations that we need to add
- @Target: It allows us to specify exactly which kind of Java element the annotation will be valid to be used. We need to add ElementType. For classes,
  it is "*ElementType.TYPE*".

  Note that if we want the annotation to be applicable over any Java element, we don't need to add Target.

  <img width="869" alt="Screenshot 2024-07-25 at 10 26 45 PM" src="https://github.com/user-attachments/assets/40806003-4877-4d62-921d-c21fd3a6f2d9">

  We would notice that there's no error when we apply the annotation to a class.

  <img width="855" alt="Screenshot 2024-07-25 at 10 28 42 PM" src="https://github.com/user-attachments/assets/4ced88ed-8fcd-48af-8cd3-5ba027945ee8">

  Over anything else, we would get an error.

  <img width="931" alt="Screenshot 2024-07-25 at 10 29 20 PM" src="https://github.com/user-attachments/assets/ab4f6433-cf24-421c-8c2d-ff95abf3cd9c">

  We can add multiple ElementTypes if needed.

  <img width="869" alt="Screenshot 2024-07-25 at 10 30 22 PM" src="https://github.com/user-attachments/assets/9643da76-c7cb-44f5-84de-9bf13007eb13">

- @Retention: This is more obscure and tough to understand at first. Most of the time, we would use it at Runtime. Runtime tells Java to keep
  this annotation around to rule the actual running of our program so that other code can actually look at that annotation and use it while the
  program is running.

  <img width="1038" alt="Screenshot 2024-07-25 at 10 32 20 PM" src="https://github.com/user-attachments/assets/34e8fec3-3272-49ff-be7a-b26b49d0f9d5">

  Other possible values are SOURCE & CLASS.

  - SOURCE means Java will get rid of this annotation before it even starts to compile our code. So that is only used for annotations that only
    matter before the code is even compiled.

    Eg: @SuppressWarning

  - CLASS means Java will keep our annotation around through compilation but once our program actually starts up i.e. at Runtime, it will get rid
    of it.

  - RUNTIME means Java keeps this annotation around throughout the actual running of the program and we can access this annotation while the
    program is running.










