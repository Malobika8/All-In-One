# Garbage Collection

Java is known as a "*Garbage Collected Language*". There are a lot of aspects of Memory Management that Java takes care of.
Overall, the function of the Garbage Collector is to delete objects from memory that our program doesn't need anymore. Without some mechanism 
for doing that, our program would accumulate more & more objects in memory over time and we would quickly run out of memory.

## How exactly does it figure out what objects our program doesn't need?

At a high level, it's simple. 

Consider the below program.

<img width="1011" alt="Screenshot 2024-07-26 at 1 06 44 PM" src="https://github.com/user-attachments/assets/d0958e84-a5a9-4586-a561-06a18fa0cbd7">

In Java, when we create and instantiate a new variable, in memory, the variable actually points to the object created.

<img width="942" alt="Screenshot 2024-07-26 at 1 12 54 PM" src="https://github.com/user-attachments/assets/0fc197f1-ed22-4bcb-bb48-49b6df5c0a18">

If some part of our program, either our variable or some object has a reference to an object in memory, it doesn't become a target for Java's
garbage collection (as long as it is still accessed).

In our program, the scope of the "*myCat*" variable is limited to *doCatStuff()* method. Once it comes out of the scope, the "*myCat*" variable 
doesn't exist and hence the reference doesn't exist as well.

<img width="952" alt="Screenshot 2024-07-26 at 1 19 40 PM" src="https://github.com/user-attachments/assets/2988cd9d-4ad8-4a8a-8573-0049aeeb47cb">

Now, since the "*Cat*" object has no purpose and simply occupies space, the garbage collector sweeps it away.

However, a variable out of scope is not the only way in which an object can become unreachable in memory.

If we create a new Cat object, then "*myCat*" would refer to the new one and the old one would be abandoned.

<img width="1025" alt="Screenshot 2024-07-26 at 1 22 10 PM" src="https://github.com/user-attachments/assets/f7b4d437-573c-4306-980e-d55bfdb84bce">
<img width="969" alt="Screenshot 2024-07-26 at 1 22 22 PM" src="https://github.com/user-attachments/assets/5d4abb77-64e8-499c-afa6-da38f5e931f2">

The same would happen if we instantiate the variable with null.

## How does Java go about doing this Garbage Collection?

Java has a whole different bunch of garbage collection objects. Most of the time we can let Java use its default garbage collection settings.

## How does default Garbage Collection work?

Suppose that our program creates & allocates space for all different items in memory. All of these initially go to the "*Young Generation Heap*".
It holds all objects that have been created very recently. Once it starts getting full, it starts with the clean-up procedure. At that point, 
it does a "**Mark & Sweep**". 

<img width="545" alt="Screenshot 2024-07-26 at 1 29 31 PM" src="https://github.com/user-attachments/assets/a5f0bfa2-4255-41c7-b7ef-fef405cb289d">

Java checks each of these items to see if they still have any references. If they do, Java marks them as "still in use".
Once done, it removes anything that's not marked freeing up memory for additional objects that might be created in the future.

It moves the objects that stay for long in the "*Young Generation Heap*" & to the "*Old Generation Heap*". 

<img width="1069" alt="Screenshot 2024-07-26 at 1 31 20 PM" src="https://github.com/user-attachments/assets/5cfcf1e4-b6b8-4002-b303-0a3209297502">

This helps in reducing overall time.
























