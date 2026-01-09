# Q1. What is the difference between == and equals() in Java? Also explain why equals() and hashCode() must be overridden together.

### `==` vs `equals()`

### `==`

* `==` compares **references**, not content
* It checks whether **both variables point to the same object in memory**
* It does **not** look at object data

Example:

```java
String a = new String("abc");
String b = new String("abc");

System.out.println(a == b); // false
```

### `equals()`

* `equals()` compares **logical equality (content)**
* Default implementation (from `Object`) behaves like `==`
* Many classes (`String`, `Integer`, etc.) **override it** to compare fields

Example:

```java
System.out.println(a.equals(b)); // true
```

### The Contract

If:

```java
a.equals(b) == true
```

Then:

```java
a.hashCode() == b.hashCode()
```

**must be true**

Because **HashMap, HashSet, HashTable** work like this:

1. Use `hashCode()` to find the **bucket**
2. Use `equals()` to find the **exact object inside the bucket**

If `equals()` is overridden but `hashCode()` is not:

* Two equal objects may go to **different buckets**
* Collection will behave incorrectly

### Example Bug

```java
class Employee {
    int id;
    String name;

    @Override
    public boolean equals(Object o) {
        return this.id == ((Employee)o).id;
    }
}
```

```java
HashSet<Employee> set = new HashSet<>();
set.add(new Employee(1, "A"));
set.add(new Employee(1, "B"));

System.out.println(set.size()); // ❌ May print 2
```

Why?
Because `hashCode()` is not overridden.

> "`==` compares memory references, while `equals()` compares logical equality.
> When using hash-based collections, `hashCode()` is used to locate the bucket and `equals()` is used to check equality inside the bucket, which is why both must be overridden together."

---

# Q2. Write a Java class `Employee` where two employees are considered equal if their `employeeId` is the same. Override `equals()` and `hashCode()` properly.

```
import java.util.Objects;

@Getter
@Setter
@AllArgsConstructor
public class Employee {

    private int id;
    private String name;

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Employee employee = (Employee) o;
        return id == employee.id;
    }

    @Override
    public int hashCode() {
        return Objects.hash(id);
    }
}
```

---

# Q3. Explain the internal working of HashMap in Java 8. What happens when two keys have the same hashcode?

### Internal Working of `HashMap` (Java 8)

1. **Key’s `hashCode()` is called**
2. Hash is **spread** (bitwise operation) to reduce collisions
3. Bucket index is calculated using:

   ```
   (n - 1) & hash
   ```
4. Entry is stored as a **Node** in the bucket array

### What happens during collision?

* If **multiple keys map to the same bucket**:

  * Initially stored as a **LinkedList**
  * `equals()` is used to check if the key already exists

### Java 8 Optimization (Treeification)

* When:

  * Bucket size **> 8**
  * AND total capacity **≥ 64**
* LinkedList is converted into a **Red-Black Tree**

Benefits:

* Search time improves from **O(n)** → **O(log n)**

### Retrieval Flow

1. Calculate hash from key
2. Find bucket index
3. Traverse:

   * LinkedList → sequential `equals()`
   * Tree → compare + tree navigation
4. Return value

---

# Q4. Common Follow-up Questions

* Why treeification threshold is 8?
* Why minimum capacity is 64?
* Can two unequal objects have same hashcode? (Yes)
* Can two equal objects have different hashcode? (No)

## Follow-up 1: Why is the treeification threshold **8**?

> Java designers chose **8** based on performance experiments to balance memory overhead and lookup time.

### Slightly Deeper 

* For small numbers of collisions, a **LinkedList is faster**
* Tree nodes have **more memory overhead**
* At around **8 nodes**, linked list lookup cost starts becoming noticeable
* That’s where converting to a **Red-Black Tree** makes sense

👉 **It’s a design choice**, not a mathematical rule.

## Follow-up 2: Why must capacity be at least **64** before treeification?

### Key Reason

To **avoid premature treeification** caused by a small table size.

### Explanation

* Small HashMap capacity → collisions happen easily
* Instead of treeifying:

  * HashMap first tries to **resize (rehash)**
* Treeification is allowed **only when resizing won’t help anymore**

👉 This prevents unnecessary memory usage and complexity.

* **Threshold 8**:

  > “Chosen empirically to balance performance and memory overhead.”

* **Capacity 64**:

  > “To ensure collisions are genuine and not caused by small table size.”

---

# Q5. Write a small Java program that demonstrates a HashMap collision using a custom key class.

Requirements:
- Two different key objects
- Same hashCode()
- equals() returns false
- Both entries should exist in the map

```
import java.util.Objects;

class Employee {
    int id;
    String name;

    Employee(int id, String name) {
        this.id = id;
        this.name = name;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Employee e = (Employee) o;
        return id == e.id;
    }

    @Override
    public int hashCode() {
        return 1; // force collision
    }
}
```
Map Usage:
```
Map<Employee, String> map = new HashMap<>();

map.put(new Employee(2, "A"), "Emp2");
map.put(new Employee(4, "B"), "Emp4");

System.out.println(map.size()); // 2
```

---

# Q6. What is abstraction in Java? How is abstraction achieved using an abstract class and an interface?

> Abstraction is the process of **exposing only what an object does and hiding how it does it**.

* Focuses on **behavior**, not data hiding
* Answers **“what”**, not **“how”**

## How Abstraction Is Achieved in Java

### 1️⃣ Using **Abstract Classes**

* Can contain:

  * Abstract methods (no body)
  * Concrete methods
  * Instance variables
* Represents an **“is-a” relationship**
* Can have **partial implementation**
  
> An abstract class provides a base class with some common behavior and some abstract methods that subclasses must implement.

### 2️⃣ Using **Interfaces**

* Interface defines a **contract**
* Specifies **what methods a class must implement**
* Supports **multiple inheritance**
* From Java 8:

  * Can have `default` methods
  * Can have `static` methods

> An interface defines a standard or contract that multiple classes can implement in their own way.

### Abstract Class vs Interface (Quick Comparison)

| Feature              | Abstract Class      | Interface                   |
| -------------------- | ------------------- | --------------------------- |
| Methods              | Abstract + concrete | Abstract + default + static |
| Variables            | Instance variables  | `public static final` only  |
| Multiple inheritance | ❌ No                | ✅ Yes                       |
| Constructor          | ✅ Yes               | ❌ No                        |
| State                | ✅ Yes               | ❌ No                        |

> “Abstraction is about hiding implementation details and exposing only behavior.
> In Java, abstraction is achieved using abstract classes and interfaces. Abstract classes allow partial implementation, while interfaces define a contract that multiple classes can implement.”


---

# Q7. Can we have a constructor in an abstract class? Can we have a constructor in an interface? Why or why not?

Abstract classes can have constructors.
Even though an abstract class cannot be instantiated directly, its constructor is invoked when a concrete subclass is created. This is useful for initializing common state.

Interfaces cannot have constructors because they cannot be instantiated and do not have instance variables. An interface only defines a contract, not object state.

---

# Q8. Can an interface extend another interface? Can a class extend multiple abstract classes? Can a class implement multiple interfaces?

An interface can extend one or more interfaces
→ This allows multiple inheritance of type.

A class cannot extend multiple abstract classes
→ Java does not support multiple inheritance of classes to avoid ambiguity (diamond problem).

A class can implement multiple interfaces
→ This is how Java supports multiple inheritance behaviorally.

Multiple inheritance through interfaces is safe because interfaces do not have state, and method conflicts can be resolved explicitly.

---

# Q9. What if two interfaces have the same default method?

If multiple interfaces provide the same default method, the implementing class must override it and explicitly choose which one to call.

```
interface A {
    default void show() {}
}

interface B {
    default void show() {}
}
class C implements A, B {
    @Override
    public void show() {
        A.super.show(); // or B.super.show()
    }
}
```

---

# Q10. What is the difference between method overloading and method overriding? Explain with rules and one tricky edge case.

## Method Overloading ✅

### Definition

* Same method name
* **Different parameter list** (number, type, or order)
* Happens **within the same class** (or inheritance)

### Rules

* Compile-time polymorphism
* Return type **alone cannot differ**
* `static`, `final`, `private` methods **can be overloaded**

### Tricky Edge Case ⚠️

```java
void test(int a)
void test(Integer a)
```

Call:

```java
test(null); // ❌ compile-time error (ambiguous)
```

## Method Overriding ✅

### Definition

* Subclass provides its own implementation of a parent method
* Same method signature

### Rules

* Runtime polymorphism
* Access modifier **cannot be reduced**
* Return type can be **covariant**
* `final`, `static`, `private` methods **cannot be overridden**
* `@Override` is optional but recommended

### Tricky Edge Case ⚠️ (Static Methods)

```java
class A {
    static void show() {}
}

class B extends A {
    static void show() {}
}
```

👉 This is **method hiding**, NOT overriding.

## Clean Comparison Table 🏆

| Feature        | Overloading  | Overriding      |
| -------------- | ------------ | --------------- |
| Polymorphism   | Compile-time | Runtime         |
| Parameters     | Must differ  | Must be same    |
| Inheritance    | Not required | Required        |
| Static methods | Can overload | Cannot override |
| Return type    | Any          | Covariant only  |

---


