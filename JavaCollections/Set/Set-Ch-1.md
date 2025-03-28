## Full Set API Hierarchy

<img width="1009" alt="Screenshot 2025-03-28 at 9 07 56 PM" src="https://github.com/user-attachments/assets/b1dde49a-8311-4ae8-84bc-e1a3e3a5aa25" />

## HashSet

<img width="949" alt="Screenshot 2025-03-28 at 9 18 00 PM" src="https://github.com/user-attachments/assets/c9b3e810-700c-47c7-9bf7-daf65849e1dc" />
<img width="957" alt="Screenshot 2025-03-28 at 9 18 20 PM" src="https://github.com/user-attachments/assets/f9910dae-e3f8-4787-8b74-64ed25fb367a" />

# 🔍 **Internal Implementation of `HashSet` in Java**

`HashSet` in Java is a part of the **`java.util` package** and is built on top of **`HashMap`**. It provides an **unordered collection of unique elements** with `O(1)` average time complexity for add, remove, and contains operations.

---

## 📌 **1️⃣ Key Features of `HashSet`**
✅ **No Duplicates** – Ensures unique elements.  
✅ **Unordered Collection** – Does not maintain insertion order.  
✅ **Backed by `HashMap`** – Uses a `HashMap` internally for storage.  
✅ **Allows `null` Values** – Can store a single `null` element.  
✅ **Not Thread-Safe** – Use `Collections.synchronizedSet(new HashSet<>())` for thread safety.  

---

## ⚙ **2️⃣ How `HashSet` Works Internally**
Internally, `HashSet` is backed by a **`HashMap`**, where:
- **Each element is stored as a key** in the `HashMap`.
- A **dummy value (`PRESENT`)** is stored as the corresponding value.
- The `HashSet` operations (`add`, `remove`, `contains`) **delegate their calls to the underlying `HashMap`**.

### **🔹 Internal Structure (`HashSet<E>` in Java)**
```java
public class HashSet<E> extends AbstractSet<E> implements Set<E>, Cloneable, Serializable {
    private transient HashMap<E, Object> map; // Backed by HashMap
    private static final Object PRESENT = new Object(); // Dummy value

    public HashSet() {
        map = new HashMap<>();
    }

    public boolean add(E e) {
        return map.put(e, PRESENT) == null; // Adds element as key, returns true if new
    }

    public boolean contains(Object o) {
        return map.containsKey(o);
    }

    public boolean remove(Object o) {
        return map.remove(o) != null;
    }

    public Iterator<E> iterator() {
        return map.keySet().iterator();
    }

    public int size() {
        return map.size();
    }
}
```

---

## 🔄 **3️⃣ How `add()` Works in `HashSet`**
When `add(E e)` is called:
1. It internally calls `map.put(e, PRESENT)`.
2. `HashMap` computes the **hash value** of `e` using `hashCode()`.
3. If the hash **does not exist**, a **new entry is created** in the `HashMap`.
4. If the hash **already exists**:
   - It **checks for equality** using `equals()`.
   - If the element is **equal** to an existing one, the **value is not added** (ensuring uniqueness).
   - If it's different, it handles collisions (via chaining or tree structure).

### **🔹 Example:**
```java
HashSet<String> set = new HashSet<>();
set.add("Apple");  // Internally, map.put("Apple", PRESENT)
set.add("Banana"); // map.put("Banana", PRESENT)
set.add("Apple");  // Duplicate! Will not be added.

System.out.println(set); // Output: [Apple, Banana]
```

---

## 🔄 **4️⃣ How `remove()` Works in `HashSet`**
When `remove(E e)` is called:
1. It internally calls `map.remove(e)`.
2. If the element exists, the `key` is removed from `HashMap`, and `true` is returned.
3. If not found, `false` is returned.

### **🔹 Example:**
```java
set.remove("Apple"); // Internally calls map.remove("Apple")
System.out.println(set); // Output: [Banana]
```

---

## 🚀 **5️⃣ How `HashSet` Handles Collisions**
Since `HashSet` relies on `HashMap`, it uses the **same collision resolution strategy**:
1. **Separate Chaining (Before Java 8)** – Uses linked lists to store multiple elements in the same bucket.
2. **Balanced Tree (Since Java 8)** – Converts linked lists into **Red-Black Trees** when bucket size > 8 for better performance.

---

## 📊 **6️⃣ Performance Analysis (`O(1)` vs `O(log n)`)**
| Operation | **Average Time Complexity** | **Worst Case (High Collisions)** |
|-----------|----------------|----------------|
| `add(E e)` | `O(1)` | `O(log n)` (tree structure) |
| `remove(E e)` | `O(1)` | `O(log n)` |
| `contains(E e)` | `O(1)` | `O(log n)` |
| `size()` | `O(1)` | `O(1)` |

✔ **Efficient for large datasets**  
✔ **Performance remains stable unless hash collisions increase drastically**  

---

## 🔥 **7️⃣ `HashSet` vs. Other Set Implementations**
| Feature | `HashSet` | `LinkedHashSet` | `TreeSet` |
|---------|----------|---------------|---------|
| **Ordering** | ❌ No order | ✅ Insertion order | ✅ Sorted order |
| **Performance (add, remove, contains)** | ⚡ `O(1)` | ⚡ `O(1)` | 🐢 `O(log n)` |
| **Underlying Data Structure** | `HashMap` | `LinkedHashMap` | `TreeMap` (Red-Black Tree) |
| **Allows `null` Values?** | ✅ Yes | ✅ Yes | ❌ No |

---

## 🎯 **8️⃣ When Should You Use `HashSet`?**
✅ **Fast Lookups & Inserts** – If order doesn't matter and you need quick searches (`O(1)`).  
✅ **Ensuring Uniqueness** – When duplicates must be avoided.  
✅ **Handling Large Datasets** – Efficient memory usage compared to `TreeSet`.  

### **📌 Why Do We Need `HashSet` If It Uses `HashMap` Internally?**  
Although `HashSet` is backed by `HashMap`, it serves a **specific purpose**: **storing a collection of unique elements without values**.  

✔ **Cleaner API** – Instead of dealing with key-value pairs (`HashMap`), we just work with values (`HashSet`).  
✔ **Encapsulation** – It hides the complexity of managing a `HashMap`, making it easier to use.  
✔ **Optimized for Set Operations** – `HashSet` directly provides methods tailored for set operations like `add()`, `remove()`, `contains()`, and `size()` without dealing with key-value mappings.  

---

### **🔍 How Does `HashSet` Ensure No Duplicates?**
**The uniqueness in `HashSet` is ensured because it stores elements as keys in `HashMap`**, and **keys in a `HashMap` must be unique**.  

#### **🔹 How It Works Internally?**
1. When you add an element to a `HashSet`, it internally calls:
   ```java
   map.put(element, PRESENT);
   ```
   - Here, `element` is the **key**, and  
   - `PRESENT` is a constant dummy value (`new Object()`).
   
2. **If the key (element) is already present**, `HashMap.put()` **replaces the old value but does not create a new entry** → thus **ensuring uniqueness**.  
3. If the key is **not present**, it is added as a new key.

---

### **📝 Example: How `HashSet` Avoids Duplicates**
```java
HashSet<String> set = new HashSet<>();
set.add("Apple");  // Internally: map.put("Apple", PRESENT);
set.add("Banana"); // Internally: map.put("Banana", PRESENT);
set.add("Apple");  // Duplicate! map.put() does not create a new entry.

System.out.println(set); // Output: [Apple, Banana]
```
Here, `"Apple"` is **not added twice** because `HashMap` **does not allow duplicate keys**.

---

### **🆚 Why Not Just Use `HashMap` Directly?**
Yes, you **could** technically use a `HashMap` directly, like this:
```java
HashMap<String, Object> map = new HashMap<>();
map.put("Apple", new Object());
map.put("Banana", new Object());
```
But using `HashSet` instead of `HashMap` provides:  
✅ A **simpler API** (no need to deal with dummy values).  
✅ **Code readability** (we clearly indicate we want a set, not a map).  
✅ **Encapsulation** (prevents misuse of key-value mapping).  

---

### **🎯 Key Takeaways**
✔ `HashSet` **exists** because it provides a **cleaner way** to store **unique elements**, unlike `HashMap`, which works with key-value pairs.  
✔ It **ensures uniqueness** because elements are stored as **keys in `HashMap`**, and **keys in a `HashMap` must be unique**.  
✔ It is **easier to use** than directly managing a `HashMap` for set operations.  

