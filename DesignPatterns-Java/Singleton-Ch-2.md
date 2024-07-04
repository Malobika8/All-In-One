## Singleton

Certain times due to certain reason, we want to enforce that a person can create only one object.
- This design pattern allows us to enforce the creation of only one object
- Delivering a single instance to everyone whoever needs it

#### Example: 
- Database connection (We do not actually need mutiple database connections)
- Logger
- ThreadPool
- Configuration Manager
- Cache Manager

Generally this is used when we have classes with costly shared resources.

### How to implement?

suppose we have a class called DatabaseConnection with certain properties.  

How to create an object for this? We can create with "new" as many time as we want.

*But how can we stop anybody to create objects this way multiple times?*

What if we make our Constructor private? Yes then nobody will be able to create any object outside of the class.
But in this scenario will we be able to create one? - No. In this scenario, even creation of one is not allowed outside the class. We can create getInstance() method. but we would need to 
create the object of the method.
so to create the object, we need to call this method and to call the method we need to call the object.

<img width="582" alt="Screenshot 2024-07-04 at 8 07 26 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d6320936-6989-4432-93bb-84818d3597bc">

How to resolve? - We can make "getInstance()" method static.

<img width="559" alt="Screenshot 2024-07-04 at 8 09 39 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d7fc3c3b-cb03-4711-91ac-777a0f75eb35">

But even in this case, we can still call this method multiple times and create multiple objects.

We can check if we have already created an object, we can send the same object instead of sending a new one. We can store the object the first time we create.

<img width="626" alt="Screenshot 2024-07-04 at 8 12 45 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/1b7ca0a1-0e1d-49cc-9c22-fe473a81f28c">

Now, even if getInstance is called multiple times, the same object instance will be sent.

There is still one concern. Even before the object is created, we want to use it. so we need to make it static as well. Or private static final.

<img width="630" alt="Screenshot 2024-07-04 at 8 14 54 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2e6a425c-b620-4f37-84f4-36daad6194da">

Lazy Instantiation:

<img width="640" alt="Screenshot 2024-07-04 at 8 20 19 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/6ed2a8be-69f2-40b6-93a1-c4c84062ce5e">

```
Note: This only works in single threaded environment.
```
Eager Instantiation:

<img width="640" alt="Screenshot 2024-07-04 at 8 20 36 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/5251e0e7-e5eb-49aa-99a7-1c59216388b9">

Con: While testing. It is difficult to test.

Some other versions:
<img width="600" alt="Screenshot 2024-07-04 at 8 22 33 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/57b5b441-035e-48c8-9fdf-821ff41c3a9f">
