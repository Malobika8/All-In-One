## 🧺 Java 9: **Collection Factory Methods**

Before Java 9, creating unmodifiable collections was verbose:

```java
List<String> list = Collections.unmodifiableList(Arrays.asList("a", "b", "c"));
```

### 🔥 Java 9 simplifies this:

#### ✅ `List.of(...)`

#### ✅ `Set.of(...)`

#### ✅ `Map.of(...)` and `Map.ofEntries(...)`

---

### ✅ Example 1: `List.of(...)`

```java
List<String> fruits = List.of("apple", "banana", "mango");
```

* Creates an **immutable** list
* Throws `UnsupportedOperationException` if you try to add/remove

---

### ✅ Example 2: `Set.of(...)`

```java
Set<String> colors = Set.of("red", "green", "blue");
```

* Also **immutable**
* Throws `IllegalArgumentException` if you add **duplicates**

---

### ✅ Example 3: `Map.of(...)`

```java
Map<String, Integer> ageMap = Map.of("Alice", 30, "Bob", 25);
```

* Can be used for up to **10 key-value pairs**

---

### ✅ Example 4: `Map.ofEntries(...)` for more than 10 pairs

```java
Map<String, Integer> map = Map.ofEntries(
    Map.entry("A", 1),
    Map.entry("B", 2),
    Map.entry("C", 3)
);
```

---

### ⚠️ Important Notes:

| Behavior                          | Outcome                           |
| --------------------------------- | --------------------------------- |
| Modifying the returned collection | ❌ `UnsupportedOperationException` |
| Null values/keys                  | ❌ `NullPointerException`          |
| Duplicate keys in `Map.of(...)`   | ❌ `IllegalArgumentException`      |

---

