# Interface Segregation Principle

```
No client should be forced to implement an interface that it doesn't use
```
An interface should be focused. If it has too many unrelated methods, it forces implementing classes to provide useless or dummy implementations.

✅ Prefer many small, specific interfaces over one fat interface.

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

---

## 💬 Questions:

🗣️ **Q:** What is the Interface Segregation Principle?

✅ *It means interfaces should be specific to what the client needs. Classes shouldn't be forced to implement unnecessary methods.*

🗣️ **Q:** How do you apply ISP in real projects?

✅ *By breaking down large service interfaces into small focused ones, and using composition to build behavior.*

🗣️ **Q:** Where does Spring follow ISP?

✅ *Spring Data repositories like `CrudRepository`, `PagingAndSortingRepository`, `JpaRepository` are layered interfaces — you implement only what you need.*

---

## 🔍 **Question:**

You are designing an interface for a **multifunctional printer**.

Here’s the current interface:

```java
public interface Machine {
    void print();
    void scan();
    void fax();
}
```

Now, you have **three** classes:

1. `MultiFunctionPrinter` – supports all features
2. `OldPrinter` – only supports **print**
3. `PhotoCopier` – supports **print and scan**, but not fax

### **Tasks:**

1. Does this `Machine` interface violate Interface Segregation Principle?
2. If yes, how would you **refactor** the interfaces to follow ISP?
3. How would you structure these three classes?

### Sol:

🔴 ISP Violation:

* `OldPrinter` is forced to implement `scan()` and `fax()` unnecessarily.
* `PhotoCopier` is forced to implement `fax()` it doesn't use.

```java
public interface Printer {
    void print();
}

public interface Scanner {
    void scan();
}

public interface FaxMachine {
    void fax();
}
```
```java
public class MultiFunctionPrinter implements Printer, Scanner, FaxMachine {
    public void print() {
        System.out.println("Printing...");
    }

    public void scan() {
        System.out.println("Scanning...");
    }

    public void fax() {
        System.out.println("Faxing...");
    }
}
```
```java
public class OldPrinter implements Printer {
    public void print() {
        System.out.println("Old printer printing...");
    }
}
```
```java
public class PhotoCopier implements Printer, Scanner {
    public void print() {
        System.out.println("Photocopier printing...");
    }

    public void scan() {
        System.out.println("Photocopier scanning...");
    }
}
```

---

## Summary:

| ✅ Principle Applied                           | ✅ Benefit                                                     |
| --------------------------------------------- | ------------------------------------------------------------- |
| Separated interfaces                          | No unnecessary method implementations                         |
| Each class chooses only the behavior it needs | High cohesion, low coupling                                   |
| Easy to extend in future                      | Add `EmailMachine` or `CloudPrinter` interfaces independently |


