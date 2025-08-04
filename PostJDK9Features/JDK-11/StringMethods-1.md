### ✅ Feature 1: **New String Methods**

Java 11 added some **super handy methods** to the `String` class:

| Method                               | Purpose                                             |
| ------------------------------------ | --------------------------------------------------- |
| `isBlank()`                          | Checks if string is empty or whitespace             |
| `strip()`                            | Removes leading/trailing whitespace (Unicode-aware) |
| `stripLeading()` / `stripTrailing()` | Self-explanatory                                    |
| `lines()`                            | Returns a Stream of lines in the string             |
| `repeat(int)`                        | Repeats the string n times                          |

---

### ✅ Example:

```java
String text = "  \tJava 11  \n";

System.out.println(text.isBlank());         // false
System.out.println("   ".isBlank());        // true
System.out.println(text.strip());           // "Java 11"
System.out.println("Line1\nLine2".lines().count());  // 2
System.out.println("Hi!".repeat(3));        // "Hi!Hi!Hi!"
```

---

### Question:

Write code that:

1. Takes the string `"   java  "` (with spaces)
2. Prints:

   * Whether it’s blank
   * The result of `strip()`
   * The result of `repeat(2)`

```
public class Main {
    public static void main(String[] args) {
        String str = "   java   ";

        System.out.println("isBlank: " + str.isBlank());         // false
        System.out.println("strip: '" + str.strip() + "'");      // 'java'
        System.out.println("repeat: " + str.strip().repeat(2));  // javajava
    }
}
```

