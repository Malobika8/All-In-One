# Interface Segregation Principle

```
No client should be forced to implement an interface that it doesn't use
```

One fat interface need to be split to many smaller and relevant interfaces so that clients can know about the interfaces that are relevant
to them. 

The ISP was first used and formulated by Robert C. Martin while consulting for Xerox.

Consider an Interface *Restaurant*. It has both *vegMeals()* and *nonVegMeals()*.

<img width="725" alt="Screenshot 2024-07-05 at 12 44 47 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/19e1adb3-4737-4be9-bbbb-70c47254f852">

Now, suppose there is *ABCVegRestaurant* that implements *Restaurant*. Now, even though it is not required, it is now forced to implement 
*nonVegMeals()* as well although it's a **Veg** Restaurant.

<img width="950" alt="Screenshot 2024-07-05 at 12 48 46 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2ff68c3b-d460-4cc9-9bdf-e2ae2b715ecb">

So, instead of combining Veg and Non-Veg Meals, segregation principle says to split the Interface into multiple parts so that everybody can
implement what they want.

We can segregate in a better way.

<img width="915" alt="Screenshot 2024-07-05 at 12 51 49 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2bd63101-0484-4bfb-add3-8c0a134d0a31">

Now, *ABCVegRestaurant* can only implement *VegRestaurent* and thus not forced to implement *nonVegMeals()*.

<img width="934" alt="Screenshot 2024-07-05 at 12 53 25 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d110da40-0a96-4b8d-a8df-82d11bf6fd24">

If some Restaurant wants both, they can implement both.

<img width="995" alt="Screenshot 2024-07-05 at 12 54 07 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/e2cff08a-009d-4521-bc77-d9759316ec7c">

