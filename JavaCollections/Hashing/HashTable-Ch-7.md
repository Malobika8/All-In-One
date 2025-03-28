## How HashTable works Internally? HashTable vs HashMap

<img width="904" alt="Screenshot 2025-03-28 at 6 27 53 PM" src="https://github.com/user-attachments/assets/5df7b702-9655-4108-91eb-a4da98737022" />
<img width="995" alt="Screenshot 2025-03-28 at 6 33 01 PM" src="https://github.com/user-attachments/assets/75b01295-03d2-41a4-8252-ca78dd6ae9ef" />

## 🔍 **How `Hashtable` Works Internally?**
`Hashtable` is one of Java’s oldest **hash-based collections**, designed for **thread safety**. Internally, it works similarly to `HashMap`, but with key differences.

---

## ⚙ **1️⃣ Internal Structure of `Hashtable`**
- Uses **an array of buckets** (like `HashMap`).
- Each bucket contains a **linked list of key-value pairs** (before Java 8).
- In **Java 8+, it does NOT use tree-based balancing** (unlike `HashMap`).
- Uses **synchronization** to ensure thread safety.

### 🔹 **Internal Representation of `Hashtable`**
```
Buckets (Array) → Linked List of Entries
   0  →  (Key1, Value1) → (Key2, Value2)
   1  →  (Key3, Value3)
   2  →  (Key4, Value4) → (Key5, Value5)
```
Each entry contains:
```java
static class Entry<K, V> {
    final K key;
    V value;
    final int hash;
    Entry<K, V> next; // Pointer to next entry in same bucket
}
```
✔ **Uses separate chaining with linked lists** for collision handling.

---

## 🔄 **2️⃣ Operations & Time Complexity**
| Operation  | Time Complexity | Notes |
|------------|---------------|------|
| **put(K, V)** | **O(1) avg, O(n) worst** | Uses hash function to find bucket. |
| **get(K)** | **O(1) avg, O(n) worst** | Searches in the bucket's linked list. |
| **remove(K)** | **O(1) avg, O(n) worst** | Deletes key and re-links the list. |
| **iteration** | **O(n)** | Iterates over all buckets sequentially. |

🚨 **Unlike `HashMap`, `Hashtable` is synchronized, making it slower in multi-threaded environments.**

---

## 🔥 **3️⃣ `Hashtable` vs. `HashMap`**
| Feature | `Hashtable` (🔒) | `HashMap` (⚡) |
|---------|--------------|--------------|
| **Thread Safety** | ✅ Yes (synchronized methods) | ❌ No (Use `ConcurrentHashMap` instead) |
| **Performance** | 🚫 Slower (synchronized) | ⚡ Faster |
| **Null Keys/Values?** | ❌ No null keys/values | ✅ Allows 1 null key & multiple null values |
| **Iteration Order** | ❌ No order guarantee | ❌ No order guarantee |
| **Collision Handling** | ✅ Linked List (Java 8-) | ✅ Linked List → Red-Black Tree (Java 8+) |

---

## 🚀 **4️⃣ When to Use `Hashtable`?**
✔ **Use `ConcurrentHashMap` instead** → `Hashtable` is outdated and inefficient.  
✔ **Use `Hashtable` only if legacy code requires it.**  

