## TreeMap

<img width="971" alt="Screenshot 2025-03-28 at 6 07 16 PM" src="https://github.com/user-attachments/assets/8513a7bd-fa2d-4186-ae8c-bf19f4566084" />
<img width="939" alt="Screenshot 2025-03-28 at 6 20 26 PM" src="https://github.com/user-attachments/assets/5180fb78-10e6-4244-b6f9-51d69040d986" />

*Red Black tree*

<img width="1030" alt="Screenshot 2025-03-28 at 6 08 35 PM" src="https://github.com/user-attachments/assets/71e5537e-22ee-47c5-bc5b-606f25927d75" />
<img width="974" alt="Screenshot 2025-03-28 at 6 19 19 PM" src="https://github.com/user-attachments/assets/bc8fc9d6-22bb-4efa-8d2c-f8cca05f7d7b" />

**`TreeMap` is implemented as a balanced binary tree, specifically a** **Red-Black Tree**. 🌳🔥  

---

## 📌 **1️⃣ How Does `TreeMap` Work Internally?**
- `TreeMap` is based on **Red-Black Tree**, a self-balancing binary search tree.  
- It maintains **sorted order** of keys (natural order or custom `Comparator`).  
- Unlike `HashMap`, which uses a **hash table**, `TreeMap` uses a **tree structure** for fast lookups.

---

## ⚙ **2️⃣ TreeMap Operations & Time Complexity**
| Operation  | Time Complexity | How? |
|------------|---------------|------|
| **put(K, V)** | **O(log n)** | Inserts into the Red-Black Tree, balancing if needed. |
| **get(K)** | **O(log n)** | Follows tree structure to find key. |
| **remove(K)** | **O(log n)** | Deletes key, then rebalances tree. |
| **iteration** | **O(n)** | In-order traversal gives **sorted keys**. |

✔ **All operations are O(log n), unlike `HashMap` where average case is O(1) but worst case can be O(n).**  

---

## 🔍 **3️⃣ Example of Internal Red-Black Tree in `TreeMap`**
If we insert:  
```java
TreeMap<Integer, String> map = new TreeMap<>();
map.put(5, "Five");
map.put(3, "Three");
map.put(8, "Eight");
map.put(1, "One");
map.put(4, "Four");
```
🔹 **Tree Structure (Balanced Red-Black Tree)**  
```
        5 (Black)
       /    \
   3 (Red)  8 (Black)
  /  \    
1(B)  4(B)
```
✔ **Sorted order is always maintained (`1, 3, 4, 5, 8`).**  
✔ **Self-balancing ensures O(log n) search time.**  

---

## 🏆 **4️⃣ `TreeMap` vs. `HashMap` vs. `LinkedHashMap`**
| Feature | `TreeMap` (🌳) | `HashMap` (⚡) | `LinkedHashMap` (📜) |
|---------|--------------|--------------|----------------|
| **Ordering** | ✅ Sorted (by keys) | ❌ No order | ✅ Insertion order |
| **Lookup Time** | ⏳ O(log n) | ⚡ O(1) avg, O(n) worst | ⚡ O(1) avg |
| **Memory Overhead** | 🏋️‍♂️ High (Tree nodes) | 🏋️‍♂️ Medium | 🏋️‍♂️ High (Linked list pointers) |
| **Best Use Case** | **Sorted data, range queries** | **Fast lookups** | **Predictable iteration** |

---

## 🚀 **Final Answer**
✔ **`TreeMap` is implemented as a Red-Black Tree.**  
✔ **It maintains keys in sorted order.**  
✔ **Operations (insert, delete, search) take O(log n).**  
✔ **Use `TreeMap` when sorting is important, but `HashMap` is faster for general key-value lookups.**  

