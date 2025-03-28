## Vector

<img width="1053" alt="Screenshot 2025-03-28 at 7 26 01 PM" src="https://github.com/user-attachments/assets/2c0669b1-d793-401d-89ec-86d240d39fd6" />
<img width="927" alt="Screenshot 2025-03-28 at 7 26 40 PM" src="https://github.com/user-attachments/assets/84f78c42-9ffa-423e-abaa-06c4e70b3ee7" />
<img width="936" alt="Screenshot 2025-03-28 at 7 28 08 PM" src="https://github.com/user-attachments/assets/3ab0664f-7f4e-4238-bf07-ac2b92761b42" />

# 🚀 **Java `Vector` - A Complete Overview**  

`Vector` is a **thread-safe, resizable array implementation** in Java that grows dynamically when needed. It is similar to `ArrayList` but **synchronizes all its methods**, making it safe for multi-threaded environments.  

---

## 🔍 **1️⃣ Key Features of `Vector`**  
✅ **Thread-safe:** All methods are `synchronized`, ensuring only one thread can modify it at a time.  
✅ **Resizable:** Automatically expands when full (default **2x growth**).  
✅ **Legacy Class:** Introduced in **Java 1.0**, before `ArrayList`.  
✅ **Implements `List`, `Cloneable`, and `Serializable`** interfaces.  

📌 **When to Use?**  
✔ Use `Vector` **only if multiple threads need safe access** to a list. Otherwise, `ArrayList` is preferred due to better performance.  

---

## ⚙ **2️⃣ Internal Working of `Vector`**  
- Internally uses an **array (`elementData[]`)** to store elements.  
- When full, it **doubles its capacity** (`capacity * 2`).  
- Supports **random access (`O(1)`)** but slower than `ArrayList` due to synchronization overhead.  

### 🔹 **Example: `Vector` Resizing Mechanism**
```java
Vector<Integer> vector = new Vector<>(3); // Initial capacity = 3
vector.add(10);
vector.add(20);
vector.add(30);
vector.add(40); // Capacity increases to 6 (doubles)

System.out.println("Size: " + vector.size());        // Output: 4
System.out.println("Capacity: " + vector.capacity());// Output: 6
```

---

## 📜 **3️⃣ Important Methods in `Vector`**
| Method | Description |
|--------|-------------|
| `add(E e)` | Adds an element at the end. |
| `add(int index, E e)` | Inserts an element at a specific position. |
| `remove(Object o)` | Removes the first occurrence of the element. |
| `get(int index)` | Returns the element at the given index. |
| `size()` | Returns the current size of the vector. |
| `capacity()` | Returns the current capacity of the vector. |
| `clear()` | Removes all elements. |
| `isEmpty()` | Checks if the vector is empty. |

### 🔹 **Example: Basic Usage of `Vector`**
```java
import java.util.Vector;

public class Main {
    public static void main(String[] args) {
        Vector<String> vector = new Vector<>();
        vector.add("Apple");
        vector.add("Banana");
        vector.add("Cherry");

        System.out.println(vector); // Output: [Apple, Banana, Cherry]
    }
}
```

---

## 🔄 **4️⃣ `Vector` vs. `ArrayList`**
| Feature | `Vector` (🔒) | `ArrayList` (🚀) |
|---------|--------------|----------------|
| **Thread Safety** | ✅ Yes (Synchronized) | ❌ No (Not Synchronized) |
| **Performance** | ⏳ Slower due to locks | ⚡ Faster (No locks) |
| **Growth Strategy** | 📈 Doubles (`capacity * 2`) | 📈 Grows by 1.5x (`capacity * 1.5`) |
| **Iterator Type** | 🚧 `Enumeration` (legacy) | ✅ `Iterator` |

🚀 **Alternative:** Instead of `Vector`, use:
```java
List<Integer> list = Collections.synchronizedList(new ArrayList<>());
```

---

## ⚠ **5️⃣ Common Pitfalls of `Vector`**
❌ **Synchronization Overhead:** Slower than `ArrayList`.  
❌ **No Fail-Fast Iteration:** Modifying while iterating can cause `ConcurrentModificationException`.  
❌ **Not Recommended for Modern Java:** `ArrayList` + external synchronization (`Collections.synchronizedList`) is preferred.  

---

## 🎯 **6️⃣ When Should You Use `Vector`?**
✅ If **multiple threads** access a list **frequently**.  
✅ If **synchronization is mandatory** and you cannot use `Collections.synchronizedList()`.  
✅ If working with **legacy code** that still relies on `Vector`.  

