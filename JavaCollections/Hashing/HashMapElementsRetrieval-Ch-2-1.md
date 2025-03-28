When you print a `HashMap` in Java (e.g., `System.out.println(map);`), the `toString()` method of `HashMap` is called, which internally **iterates over all entries** in the map.  

But how does it fetch the elements? 🤔 Let’s break it down.

---

## 🔍 **1️⃣ How Does `HashMap` Fetch Elements When Printed?**
- **Internally, `HashMap` uses an array of buckets (`Node<K, V>[] table`).**
- **Iteration starts from the first non-null bucket (index 0) and goes up to the last bucket.**
- **Inside each bucket, elements are retrieved in order (linked list or tree structure).**
  
### 🔹 **Example: Printing a `HashMap`**
```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        HashMap<Integer, String> map = new HashMap<>();
        map.put(2, "Two");
        map.put(1, "One");
        map.put(3, "Three");
        map.put(4, "Four");

        System.out.println(map); // Prints elements in arbitrary order
    }
}
```
🔸 **Possible Output:**  
```
{1=One, 2=Two, 3=Three, 4=Four}  // Order depends on hash codes & bucket placement
```

---

## ⚙ **2️⃣ Step-by-Step: How `HashMap` Iterates When Printed**
- `HashMap` **does NOT maintain insertion order** (unlike `LinkedHashMap`).
- It **iterates over the internal array (`table[]`) from index `0` to `n-1`.**
- If a bucket contains multiple entries (due to collisions), they are retrieved **in the order they were inserted within that bucket.**
- If a bucket has been treeified (in Java 8+), it follows **Red-Black Tree order** (sorted by key).

🔹 **Inside `HashMap.toString()`**
```java
public String toString() {
    Iterator<Map.Entry<K, V>> it = entrySet().iterator();
    StringBuilder sb = new StringBuilder("{");
    while (it.hasNext()) {
        Map.Entry<K, V> e = it.next();
        sb.append(e.getKey()).append("=").append(e.getValue());
        if (it.hasNext()) sb.append(", ");
    }
    return sb.append("}").toString();
}
```
📌 **Key Takeaway:** It relies on the `entrySet()` iterator.

---

## 🏗 **3️⃣ Example: How HashMap Iterates Internally**
```java
HashMap<Integer, String> map = new HashMap<>();
map.put(10, "Ten");
map.put(20, "Twenty");
map.put(30, "Thirty");
map.put(40, "Forty");

System.out.println(map); 
```
✅ **Internal Structure (Assume Hash Collisions)**  
```
Bucket[0] -> (10, "Ten") → (30, "Thirty")
Bucket[1] -> (20, "Twenty")
Bucket[2] -> (40, "Forty")
```
🔹 **Iteration Order (Depends on Hash Placement)**
```
{10=Ten, 30=Thirty, 20=Twenty, 40=Forty}  (Example output)
```
🚨 **Order may change due to hash distribution, collisions, and resizing.**

---

## 🏆 **4️⃣ `HashMap` Iteration Order vs. Other Maps**
| **Map Type** | **Iteration Order** |
|-------------|--------------------|
| **HashMap** | ❌ Unpredictable order (Depends on hash function) |
| **LinkedHashMap** | ✅ Maintains insertion order |
| **TreeMap** | ✅ Sorted order (by natural/comparator order) |

