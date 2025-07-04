### 🧠 **Topic 1: Lambda Expressions (Java 8 Core Feature)**

#### ✅ **Intro for Notes:**

Lambda expressions were introduced in Java 8 to enable **functional programming**. They allow you to treat **functions as first-class citizens**, making your code more concise and readable. Instead of using anonymous inner classes, you can write functional interfaces with simple syntax like `(args) -> expression`.

**Syntax:**

```java
(parameter1, parameter2) -> { // body }
```

Used commonly with **functional interfaces** (interfaces with only one abstract method), like `Runnable`, `Comparator`, or custom ones.

---

### 💻 **Question 1: Basic Lambda Usage**

Write a lambda expression that:

1. Takes two integers.
2. Returns their sum.

**Instructions:**

* Define a functional interface `Adder`.
* Use a lambda to implement the interface.
* Print the result of adding two numbers using the lambda.

**Code**
```
public class Test {
    public static void main(String[] args){
        Adder<Integer, Integer, Integer> func = (n1, n2) -> n1+n2;
        System.out.println(func.add(2, 3));
    }
}

@FunctionalInterface
interface Adder<T,U,R>{

    public R add(T t, U u);
}
```
