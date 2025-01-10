# Abstract Classes

## Methods

In Java, **abstract methods** are typically declared `public` or `protected`. However, there are specific rules regarding their visibility:

1. **Abstract methods must be at least as accessible as the class that declares them.**
   - If a class is `public`, its abstract methods should also be `public` or `protected` (but not private).
   - If a class is `package-private` (no modifier), the abstract methods can be package-private, `protected`, or `public`.

2. **Private abstract methods are not allowed.**
   - Since abstract methods are meant to be overridden by subclasses, making them `private` would make no sense because `private` members are not visible to subclasses.

### Example: Valid abstract method declarations
```java
public abstract class Animal {
    public abstract void makeSound(); // public abstract method
}

abstract class Plant {
    protected abstract void grow(); // protected abstract method
}

abstract class Machine {
    abstract void operate(); // package-private (default) abstract method
}
```

### Example: Invalid abstract method declaration
```java
public abstract class Vehicle {
    private abstract void move(); // Compilation error: abstract methods cannot be private
}
```

### Why are abstract methods typically `public` or `protected`?
- **Purpose of abstraction**: Abstract methods define a contract for subclasses. To fulfill this contract, subclasses must have access to these methods, which is only possible if the methods are at least `protected`.

## Properties

Yes, **abstract classes** in Java can have **properties (fields)**. These properties can be:

1. **Instance Variables** (with or without access modifiers)
2. **Static Variables**
3. **Final Variables**

However, the behavior of these properties in an abstract class is similar to regular class properties, and they can be used to provide shared data or default functionality for subclasses.

### Key Points about Properties in Abstract Classes:
1. **Instance Variables**  
   - Abstract classes can have instance variables, and these can have any access modifier (`private`, `protected`, `public`, or default).
   - These variables can be initialized in the abstract class or in its concrete subclass.

2. **Static Variables**  
   - Abstract classes can have `static` variables that belong to the class and not to any specific instance.
   - Useful for sharing constants or static data among all instances of the subclasses.

3. **Final Variables**  
   - Abstract classes can declare `final` variables (constants) that cannot be changed once initialized.

4. **Access through Methods**  
   - Abstract classes often use methods (abstract or concrete) to manipulate or expose their properties to ensure proper encapsulation.

---

### Example:

```java
public abstract class Vehicle {
    // Instance variable
    protected String brand;

    // Static variable
    public static final int MAX_SPEED = 120;

    // Constructor to initialize instance variable
    public Vehicle(String brand) {
        this.brand = brand;
    }

    // Abstract method
    public abstract void move();

    // Concrete method
    public String getBrand() {
        return brand;
    }
}
```

### Subclass Example:

```java
public class Car extends Vehicle {
    public Car(String brand) {
        super(brand);
    }

    @Override
    public void move() {
        System.out.println(brand + " is moving.");
    }
}

public class Main {
    public static void main(String[] args) {
        Car car = new Car("Toyota");
        car.move(); // Output: Toyota is moving.
        System.out.println("Max speed: " + Vehicle.MAX_SPEED);
    }
}
```

### Conclusion:
Abstract classes can have properties, and they are useful for providing shared or default functionality to subclasses. These properties can be instance variables, static variables, or constants, depending on the design needs.

## Constructors

**Abstract classes in Java** can have constructors, and here's why:

---

### Why Abstract Classes Have Constructors:

1. **To Initialize Instance Variables**:
   - Abstract classes, unlike interfaces, can have **instance variables**. These variables may need to be initialized, which is done through constructors.
   - The constructor of an abstract class is called when a concrete subclass is instantiated, allowing the abstract class to initialize its fields.

   ```java
   public abstract class Animal {
       protected String name;

       public Animal(String name) {
           this.name = name;
           System.out.println("Animal constructor called");
       }

       public String getName() {
           return name;
       }

       public abstract void makeSound();
   }

   public class Dog extends Animal {
       public Dog(String name) {
           super(name);
       }

       @Override
       public void makeSound() {
           System.out.println(name + " says: Woof!");
       }
   }

   public class Main {
       public static void main(String[] args) {
           Dog dog = new Dog("Buddy");
           dog.makeSound();  // Output: Animal constructor called
                             //         Buddy says: Woof!
       }
   }
   ```

---

2. **To Provide Common Initialization Logic**:
   - Abstract classes can define **shared initialization logic** that applies to all subclasses, avoiding code duplication.
   - Subclasses can reuse the constructor of the abstract class using the `super` keyword.

---

### Key Points:
- **Cannot Instantiate Abstract Classes Directly**:
   - You cannot create an object of an abstract class directly, but its constructor is still called when a concrete subclass is instantiated.

- **Constructors in Subclasses**:
   - When a subclass extends an abstract class, the subclass must invoke the abstract class's constructor (implicitly or explicitly) as the first statement in its own constructor.

---

### Benefits of Constructors in Abstract Classes:
1. **Encapsulation of Shared Logic**: Common initialization logic can be encapsulated in the abstract class.
2. **Reduction of Code Duplication**: Subclasses can reuse the abstract class's constructor logic.
3. **Support for Instance Variables**: Abstract classes can manage their own state, unlike interfaces.

---

### Summary:
- Abstract classes have constructors to allow initialization of their instance variables and shared logic.
- These constructors are called when a concrete subclass is instantiated, ensuring proper initialization across the class hierarchy.

