# Built-in Functional Interface

Let's use some of the existing Interfaces that are present in the Java library.

(Note: Method references are internally converted to lambda)

Suppose we want to sort. 

### Do we have built-in interfaces in Java?

We have a "*Consumer*" interface that accepts an input argument but returns nothing.

<img width="450" alt="Screenshot 2024-07-29 at 10 45 33 AM" src="https://github.com/user-attachments/assets/0247f24f-8837-4483-ac23-4b4dba435a18">
<img width="669" alt="Screenshot 2024-07-29 at 10 47 18 AM" src="https://github.com/user-attachments/assets/8e794fd6-b7f1-43b3-bf06-3596508eafc7">

Suppose we want to do a sum. The abstract method in the interface should take two inputs and return a value.
We have an interface called "*Bi-Function*".

<img width="654" alt="Screenshot 2024-07-29 at 10 48 27 AM" src="https://github.com/user-attachments/assets/e9551abb-5fb4-40d2-845d-d958edf5a73d">
<img width="1048" alt="Screenshot 2024-07-29 at 10 49 37 AM" src="https://github.com/user-attachments/assets/564911c7-75fc-451a-aa70-813a196162f9">

It can be used for any scenario.

There are multiple in-built interfaces that can be made use of. Ex: *BiPredicate*

<img width="952" alt="Screenshot 2024-07-29 at 10 53 48 AM" src="https://github.com/user-attachments/assets/34ef028a-a7e1-43c2-94ee-8439a440adc3">

We can also use "*BiFunction*" and pass the return type as Boolean.

<img width="917" alt="Screenshot 2024-07-29 at 10 55 32 AM" src="https://github.com/user-attachments/assets/b0a56c71-3aaa-4ed3-9e47-29a201e5e844">

## Questions

1. There's a method called "*hashCode()*" in the "Object" class which takes an input and returns a value. What is the existing interface that
   Do you think we could use it for this?

   <img width="948" alt="Screenshot 2024-07-29 at 10 57 13 AM" src="https://github.com/user-attachments/assets/c2f201c4-a54f-4ef4-b446-b9553ab2d1c8">

   "*Function*" interface.

   <img width="664" alt="Screenshot 2024-07-29 at 10 59 02 AM" src="https://github.com/user-attachments/assets/9f2ef3ff-d77a-480e-8a5c-add6dbf17140">
   <img width="1033" alt="Screenshot 2024-07-29 at 11 00 10 AM" src="https://github.com/user-attachments/assets/77d37847-fdbb-4b69-b612-db0c766ac701">
   <img width="677" alt="Screenshot 2024-07-29 at 11 00 20 AM" src="https://github.com/user-attachments/assets/751091c5-5956-4e74-9a08-54dfd5f214da">

   Let's say we don't want "*hashCode()*" to return anything. Can we use the "Consumer" interface? It takes one input but doesn't return anything.

   Yes as we don't care what it returns.

   <img width="959" alt="Screenshot 2024-07-29 at 11 03 52 AM" src="https://github.com/user-attachments/assets/e3278748-6ac0-47c4-9f99-80af85bb6508">

   Let's take another example.

   Suppose we want to print something. We have a "*println()*" method in "*PrintStream*" class. But it's not a static method.

   <img width="884" alt="Screenshot 2024-07-29 at 11 05 33 AM" src="https://github.com/user-attachments/assets/33fe0b5b-907a-4095-8900-963461147570">

   ### Then how do we use it?

   We have a "*System*" class that has "*in*" and "*out*" references that provide the "*PrintStream*" type value.

   <img width="717" alt="Screenshot 2024-07-29 at 11 08 05 AM" src="https://github.com/user-attachments/assets/f18f1aaf-6247-4002-a7a2-4c58301211d8">

   We can make use of this to get the PrintStream object.

   <img width="748" alt="Screenshot 2024-07-29 at 11 09 41 AM" src="https://github.com/user-attachments/assets/45efce4a-191d-4e0d-a843-badde736521f">
   <img width="607" alt="Screenshot 2024-07-29 at 11 09 44 AM" src="https://github.com/user-attachments/assets/4d285c07-3818-4fd3-9ba9-4c390187c38e">

   ## Takeaway: We cannot directly call a static method.

2. Let's say we have an interface named "*IUpperCase*".

   <img width="759" alt="Screenshot 2024-07-29 at 11 15 08 AM" src="https://github.com/user-attachments/assets/cc6b16e0-7433-48c4-9661-67df61d9cd30">

   We have a method called "*toUpperCase()*" in String. But it doesn't take an argument and is not static.

   <img width="770" alt="Screenshot 2024-07-29 at 11 16 10 AM" src="https://github.com/user-attachments/assets/f1836f3b-91f7-4425-acbb-6f4a6c173ebf">

   Even when we use it directly, it doesn't work as it's not static.
   
   <img width="560" alt="Screenshot 2024-07-29 at 11 19 55 AM" src="https://github.com/user-attachments/assets/ce5a4780-1f4c-4627-9ba7-406143355595">

   Even then, it works fine with method reference.

   ### But how?

   <img width="991" alt="Screenshot 2024-07-29 at 11 16 52 AM" src="https://github.com/user-attachments/assets/9e867716-e737-4c61-ac22-ecfe1e290ae1">
   <img width="704" alt="Screenshot 2024-07-29 at 11 18 22 AM" src="https://github.com/user-attachments/assets/00179595-3304-4975-87b1-a365c9769f5a">

   
   

   
   
   






