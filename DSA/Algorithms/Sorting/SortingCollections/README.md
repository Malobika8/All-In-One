## 🔁 Comparator in Java

The lambda you pass to `sort()` is of the form:

```java
(s1, s2) -> someValue
```

It must follow this logic:

| Return Value     | Meaning                    | Sorting Order |
| ---------------- | -------------------------- | ------------- |
| `negative` (< 0) | `s1` comes **before** `s2` | ascending     |
| `zero`           | `s1` and `s2` are equal    | no change     |
| `positive` (> 0) | `s1` comes **after** `s2`  | descending    |

> So: if `s1 - s2 > 0`, `s1` goes **after** `s2`!

---

### 🧠 So what does this mean for sorting GPAs?

Let’s say:

```java
Student s1 = Bob (3.9);
Student s2 = David (3.2);
```

If you write:

```java
(s1, s2) -> s1.getGpa() - s2.getGpa()
```

That's:

```
3.9 - 3.2 = 0.7 (positive)
```

➡️ So **Bob will come after David**, because the comparator returned positive — meaning **ascending order**.

---

### ✅ But you want **descending order**, so Bob (3.9) should come before David (3.2).

You should write:

```java
(s1, s2) -> s2.getGpa() - s1.getGpa()
```

That's:

```
3.2 - 3.9 = -0.7 (negative)
```

➡️ So **Bob comes before David** — correct for **descending order**.

---

## 🔍 Why the Confusion?

Many think:

> “If `s1 - s2` is positive, `s1` should come first!”

But **in Java Comparator**, a **positive return value** means `s1` goes **after** `s2`.

---

## ✅ Safer Alternative

Since subtraction (`double - double`) can be error-prone due to floating-point issues, always prefer:

```java
Comparator.comparingDouble(Student::getGpa).reversed()
```

or

```java
(s1, s2) -> Double.compare(s2.getGpa(), s1.getGpa())
```

This avoids incorrect ordering due to precision or edge cases.

---

### 🧪 Final Example:

```java
students.sort((s1, s2) -> Double.compare(s2.getGpa(), s1.getGpa()));
```

or:

```java
students.sort(Comparator.comparingDouble(Student::getGpa).reversed());
```

➡️ Will place students with **higher GPA first** — descending order.

---

