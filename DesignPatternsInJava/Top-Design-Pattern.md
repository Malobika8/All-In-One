These are Language agnostic but we will use Java to implement the same
Gang of FOUR: Introduced 23 design patterns

## What are Design Patterns?
Pattern: Something which frequently occurs.

They are mechanism to write a managaeble code.

We are trying to design a software. DP were introduced to certain problems.

Design Patterns are nothing but well established solutions of some commonly faced software deign problems.

## Types:
- Creational: Singleton, Builder, Factory, Abstract Factory, Prototype
- Structural: Adapter, Facade, Decorator
- Behavioral: Observer, Strategy, State, Bridge

## Creational Design patterns

We create a class and as soon as we create a class, we cannot store a data.

How do we store a data then? - We create objects.

All of the design patterns under creational talk about certain problem statements of creation of objects.

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

## Builder

It is possible that there's a class with a lot of attributes. Some are optional and some are not.
The process of object creation can be tricky in such cases.

Suppose we have a Student class. To create an object, generally two things are necessary - id, name.

But certain people want to add more info. We can add one more constructor.
Likewise, a lot of constructors with different combination of attributes would be required.

<img width="590" alt="Screenshot 2024-07-04 at 8 31 21 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/666321ac-4835-4e44-bc29-6478fa1e7aed">

One simple solution would be to use setters to set whatever we like. But there are complications with this. We would then require to know everything about the Student class to make it 
properly work. 

<img width="472" alt="Screenshot 2024-07-04 at 8 32 15 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9dd7469b-e267-490f-83f4-001ce5b48f83">

We might also have certain validation checks. validations would be done later once the object is created. It's better to stop the object creation process if validation checks doesn't pass.

<img width="514" alt="Screenshot 2024-07-04 at 8 34 39 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c35e47e1-8a40-4f24-8674-56bae363ca21">

Validaton should be done DURING object creation.

We can have a separate class(say StudentBuilder) with all the attributes and setters which can be passd to Student class. 
Our Student constructor would expect a StudentBuilder object. In that case, we won't require to provide multiple arguments in teh Student constructor. We can set whatever properties we 
want. All validations can be done in the StudentBuilder class itself.

<img width="837" alt="Screenshot 2024-07-04 at 8 48 17 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ba465d30-27aa-45bf-9399-662eb2268440">
<img width="844" alt="Screenshot 2024-07-04 at 8 50 36 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8c271d06-5b3f-4d20-8a33-68a387e9bcf0">
<img width="815" alt="Screenshot 2024-07-04 at 8 49 55 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/3eb9b8de-e812-4824-85c5-20204fce306c">
<img width="825" alt="Screenshot 2024-07-04 at 8 50 02 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/556d9280-5ac0-4aa0-a608-465006bff97f">

```
It is Backward compatible
```

let's try to make it better

We can have Student class return a StudentBuilder object rather than we create it.

<img width="833" alt="Screenshot 2024-07-04 at 8 54 28 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/821c1a48-c060-488f-bf4e-87db028f46d5">
<img width="817" alt="Screenshot 2024-07-04 at 8 55 01 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/89f24063-528a-425a-a369-e3a40d424757">

We can make it even better by letting the getter methods in Studentbuilder return StudentBuilder object(the same object back).

<img width="692" alt="Screenshot 2024-07-04 at 8 59 51 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/e9929aff-8829-431f-aedd-f3a663c5222e">

We can now use method chaining.

<img width="689" alt="Screenshot 2024-07-04 at 9 00 07 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c4b4d245-746f-48b3-a61f-4b474fad9718">

We can have a build method in StudentBuilder which can set all the attributes and return Student Object. The build method takes the StudentBuilder object and pass it to the 
Student Construtor. It can then return the same Student object.

<img width="691" alt="Screenshot 2024-07-04 at 9 03 05 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/5d757574-efbf-4558-8129-368867d30a3e">
<img width="690" alt="Screenshot 2024-07-04 at 9 03 44 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d0eb168a-b251-44bc-994f-7e191792a84d">

We can have validations in build method before creating the Student object

<img width="681" alt="Screenshot 2024-07-04 at 9 06 16 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/efa8865b-01e8-4026-ab50-2e5f9aca36c5">

We still cannot stop people from creating Student object using new keyword.
In order to stop it, we need to make the constructor private. but then we wont be able to create Student object in the StudentBuilder class.

<img width="535" alt="Screenshot 2024-07-04 at 9 07 48 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2e867936-2eb3-480d-81fc-8e10789541d9">

We can add the class in Student class itself as static inner class. This wont allow us to directly create the object of Student class.

<img width="692" alt="Screenshot 2024-07-04 at 9 10 14 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/fc98b937-03ff-4715-93e3-af5b3222d3b2">
<img width="685" alt="Screenshot 2024-07-04 at 9 09 53 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/0d4fbe05-f28e-4d46-8cff-bf17cacf307b">

#### Reference: Google's example of Builder - https://firebase.google.com/docs/reference/android/com/google/android/gms/ads/RequestConfiguration

## 




