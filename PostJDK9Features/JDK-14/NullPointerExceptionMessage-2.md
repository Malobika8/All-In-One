## ✅ Java 14 Feature: **Helpful `NullPointerException` Messages**

---

### 🔹 The Problem (Before JDK 14):

When you got a `NullPointerException`, Java used to show you only **where** it occurred — not **what** was `null`.

```java
person.getAddress().getCity();
```

❌ Old NPE message:

```
Exception in thread "main" java.lang.NullPointerException
    at MyClass.main(MyClass.java:12)
```

🙄 Not helpful — you had to guess:
Was it `person`, `person.getAddress()`, or something else?

---

### ✅ Java 14+ Solution:

Java now gives **precise messages** in `NullPointerException`:

```java
Exception in thread "main" java.lang.NullPointerException: 
    Cannot invoke "Address.getCity()" because "person.getAddress()" is null
```

🔍 It tells you:

* What method call failed
* Which exact part of the chain was `null`

---

### ✅ Example:

```java
class Address {
    String getCity() { return "Kolkata"; }
}

class Person {
    Address address;
    Address getAddress() { return address; }
}

public class Test {
    public static void main(String[] args) {
        Person person = new Person();
        String city = person.getAddress().getCity(); // 👈 NPE here
        System.out.println(city);
    }
}
```

### ✅ Output in JDK 14+:

```
Exception in thread "main" java.lang.NullPointerException: 
    Cannot invoke "Address.getCity()" because "person.getAddress()" is null
```

---

## ✅ How to Enable It (JDK 14+)

This feature is **off by default** in JDK 14 (to avoid performance overhead), but you can turn it on via JVM flag:

```bash
java -XX:+ShowCodeDetailsInExceptionMessages MyApp
```

### 🔸 From Java 15 onward, it's enabled by default ✅

---

## 🧠 Why it matters:

* Saves debugging time 🕵️‍♀️
* Especially useful for long method chains
* Reduces “guesswork” in bug fixing

---

### ✅ Summary:

| Version       | Behavior                            |
| ------------- | ----------------------------------- |
| Before JDK 14 | Only shows line number              |
| JDK 14        | Shows exact null reference (opt-in) |
| JDK 15+       | Same — but **enabled by default** ✅ |

---

