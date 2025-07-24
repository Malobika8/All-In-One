## Liskov Substitution Principle (LSP)

### ✅ **Definition (from Barbara Liskov):**

> **“Objects of a superclass should be replaceable with objects of its subclasses without affecting the correctness of the program.”**

---

### 🧠 In Simple Terms:

If class `B` is a subclass of class `A`, then we should be able to **use `B` anywhere `A` is expected**, **without breaking functionality**.

If a subclass changes the **expected behavior** of the parent, then **LSP is violated**.

---

## 🔴 Bad Example (Violates LSP):

```java
class Bird {
    public void fly() {
        System.out.println("Bird is flying");
    }
}

class Ostrich extends Bird {
    @Override
    public void fly() {
        throw new UnsupportedOperationException("Ostriches can't fly!");
    }
}
```

### Problem:

* You **can’t substitute** `Ostrich` for `Bird` without risking an exception.
* You expect `Bird.fly()` to always work — but with `Ostrich`, it doesn’t.

🧨 **LSP violation**: The subclass broke the expectation of the superclass.

---

## ✅ Good Example (Respects LSP):

### Step 1: Use correct abstraction

```java
interface Bird {
    void layEggs();
}

interface FlyingBird extends Bird {
    void fly();
}
```

### Step 2: Implement behavior safely

```java
class Sparrow implements FlyingBird {
    public void layEggs() { System.out.println("Sparrow lays eggs."); }
    public void fly() { System.out.println("Sparrow is flying."); }
}

class Ostrich implements Bird {
    public void layEggs() { System.out.println("Ostrich lays eggs."); }
}
```

✅ Now:

* We don’t force `Ostrich` to have `fly()`.
* `FlyingBird` and `Bird` are separated.
* Substitutability is preserved.

---

## Questions:

🗣️ **Q:** What is LSP?

✅ *If a class extends another class, it should be usable anywhere its parent is expected, without breaking the behavior.*

🗣️ **Q:** How does LSP differ from OCP?

✅ *LSP is about correct inheritance and substitutability; OCP is about extending behavior without modifying existing code.*

🗣️ **Q:** Have you seen LSP violations in real projects?

✅ *Yes — often when a subclass overrides a method and throws `UnsupportedOperationException`, or changes return types unexpectedly.*

---

## ✅ Real-World Spring Example (LSP Friendly)

```java
interface NotificationService {
    void notifyUser(String message);
}
```

```java
class EmailService implements NotificationService {
    public void notifyUser(String message) {
        // send email
    }
}

class SMSService implements NotificationService {
    public void notifyUser(String message) {
        // send SMS
    }
}
```

Now, you can inject `NotificationService` and use **any subclass** (email, SMS, etc.) safely.

## IMP:

**Wherever there's an expectation of Base Class object, we should be able to supply the Sub-class instances *PROVIDED IT DOESN'T BREAK THINGS*.**

---

## 🔍 **Question:**

You're designing a shape-drawing system. Here's the current code:

```java
public class Rectangle {
    private int width;
    private int height;

    public void setWidth(int width) { this.width = width; }
    public void setHeight(int height) { this.height = height; }

    public int getArea() {
        return width * height;
    }
}
```

Now someone creates a `Square` class by extending `Rectangle`:

```java
public class Square extends Rectangle {
    @Override
    public void setWidth(int width) {
        super.setWidth(width);
        super.setHeight(width);
    }

    @Override
    public void setHeight(int height) {
        super.setHeight(height);
        super.setWidth(height);
    }
}
```

And here's the test code:

```java
public class Main {
    public static void main(String[] args) {
        Rectangle rect = new Square(); // Substitution happening here
        rect.setWidth(5);
        rect.setHeight(10);
        System.out.println("Area = " + rect.getArea());
    }
}
```

### **Tasks:**

1. Is this a violation of Liskov Substitution Principle?
2. If yes, **why**?
3. How would you **redesign** this to follow LSP?

### Sol:

**Notice the confusion**, and that’s exactly what LSP violations feel like: **confusing and misleading behavior** when substituting subclasses.

#### **Is this a violation of LSP?**

**Yes.**

#### **Why is it a violation?**

```java
Rectangle rect = new Square();
rect.setWidth(5);
rect.setHeight(10);
System.out.println("Area = " + rect.getArea());
```

You expect:

```java
Area = 5 * 10 = 50
```

But since `Square.setHeight()` also sets width to 10, the actual area becomes:

```java
Area = 10 * 10 = 100 ❌
```

> ❌ This breaks the **expected behavior** of `Rectangle`.
> A class using `Rectangle` cannot safely work with `Square`.
> Therefore, **Liskov Substitution Principle is violated**.

#### **How to redesign to follow LSP?**

The root issue is **wrong inheritance**. A square **is not a subtype** of rectangle in behavioral terms.

#### Use composition instead of inheritance

#### Create a common interface

```java
public interface Shape {
    int getArea();
}
```

#### Implement `Rectangle` and `Square` separately

```java
public class Rectangle implements Shape {
    private int width;
    private int height;

    public Rectangle(int width, int height) {
        this.width = width;
        this.height = height;
    }

    public int getArea() {
        return width * height;
    }
}
```

```java
public class Square implements Shape {
    private int side;

    public Square(int side) {
        this.side = side;
    }

    public int getArea() {
        return side * side;
    }
}
```

#### Now both shapes can be used safely:

```java
public class Main {
    public static void main(String[] args) {
        Shape shape1 = new Rectangle(5, 10);
        Shape shape2 = new Square(7);

        System.out.println("Area of Rectangle: " + shape1.getArea()); // 50
        System.out.println("Area of Square: " + shape2.getArea());    // 49
    }
}
```

Now:

* No **confusing setters**
* No **override abuse**
* No **substitution problems**
* **LSP is respected**

#### Key Takeaway:

| Don't do this ❌                    | Do this ✅                        |
| ---------------------------------- | -------------------------------- |
| `Square extends Rectangle`         | `Square implements Shape`        |
| Forcing behavior through overrides | Use composition and clear models |

---

## **Question:**

You are building a vehicle management system. Here's the base class and one subclass:

```java
public class Vehicle {
    public void startEngine() {
        System.out.println("Engine started.");
    }
}
```

Now someone creates a new subclass:

```java
public class Bicycle extends Vehicle {
    @Override
    public void startEngine() {
        throw new UnsupportedOperationException("Bicycles don't have engines!");
    }
}
```

### **Tasks:**

1. Does this violate LSP? Why or why not?
2. How would you redesign it to **follow** the Liskov Substitution Principle?

### Sol:

**This violates LSP. Why?**
> *Bicycle throws exception in `startEngine()` which breaks the expected behavior of `Vehicle`.*
That’s exactly it.

If a `Vehicle` is expected to start an engine, then **all subclasses** should be able to do so. But `Bicycle` **can't** — so substituting `Vehicle vehicle = new Bicycle()` breaks things.

This violates LSP.

```java
public interface Vehicle {
    void move();
}
```
```java
public interface WithEngine extends Vehicle {
    void startEngine();
}
```
```java
public class Car implements WithEngine {
    public void startEngine() {
        System.out.println("Car engine started.");
    }

    public void move() {
        System.out.println("Car is moving.");
    }
}
```
```java
public class Bicycle implements Vehicle {
    public void move() {
        System.out.println("Bicycle is moving.");
    }
}
```
```java
public class Main {
    public static void main(String[] args) {
        Vehicle bike = new Bicycle();
        bike.move();

        WithEngine car = new Car();
        car.startEngine();
        car.move();
    }
}
```

Now:

* No unexpected exceptions
* You can substitute `Car` for `WithEngine`, and `Bicycle` for `Vehicle` safely
* ✅ LSP is respected!

---

## ✅ Summary:

| ✅ What we Did                                        | ✅ Why It's Correct             |
| ------------------------------------------------ | ------------------------------ |
| Split behavior into multiple interfaces          | Keeps subclasses substitutable |
| Avoided engine logic in Bicycle                  | Prevents LSP violation         |
| Created hierarchy that reflects **capabilities** | Clean and extensible design    |

---

