# Liskov Substitution Principle

```
Objects of Super-Class will be replaced with objects of Sub-Class.
```

Consider a Class named *vehice* which has something called *start()* & *stop()*. Consider other classes *Bike* & *Car* that extends Vehicle with its own
implementation of *start()* & *stop()* methods.

<img width="915" alt="Screenshot 2024-07-05 at 12 33 55 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8e83a121-d137-4c14-b814-ba191722613c">
<img width="776" alt="Screenshot 2024-07-05 at 12 34 14 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c16ccc7d-dc2b-471f-84f4-175fb046fd9a">
<img width="778" alt="Screenshot 2024-07-05 at 12 34 32 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7ce3ba85-7d22-41d1-bb5c-9f1cb1b898f7">

Consider another Class which has *testDrive()* method that takes *Vehicle* as argument.

<img width="778" alt="Screenshot 2024-07-05 at 12 35 03 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/96c052df-96d4-42a6-9b2c-6dbe117d6b84">

So, this particular class code is applicable for all Vehicles. We should be able to substitute the Sub-classes as well.

<img width="855" alt="Screenshot 2024-07-05 at 12 36 53 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/6689b6ce-9cf2-48b6-93c7-231c711ff9f7">

Because the argument in *testDrive()* method is of Base-class(*Vehicle*) type, it is substitutable.

<img width="955" alt="Screenshot 2024-07-05 at 12 38 53 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/f5f4a8a1-57f6-400e-9d2b-37f82ccaf77b">



## IMP:

**Wherever there's an expectation of Base Class object, we should be able to supply the Sub-class instances *PROVIDED IT DOESN'T BREAK THINGS*.**


