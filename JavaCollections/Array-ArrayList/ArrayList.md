## ArrayList

* addAll()
* clear()
* clone()
* contains()
* indexOf()
* removeIf()
* retainAll()
* subList()
* toArray()

## Remove duplicates from an ArrayList

<img width="937" alt="Screenshot 2025-03-28 at 11 00 39 AM" src="https://github.com/user-attachments/assets/51bc3aff-4ff2-4ce5-9c84-d082c836e43e" />

## Compare Two ArrayLists in Java

<img width="951" alt="Screenshot 2025-03-28 at 11 06 18 AM" src="https://github.com/user-attachments/assets/0a80d228-3d28-4684-93c5-05b98080b765" />
<img width="946" alt="Screenshot 2025-03-28 at 11 07 19 AM" src="https://github.com/user-attachments/assets/0e8f7253-6e63-4b15-800e-aa75bdf2f1de" />
<img width="937" alt="Screenshot 2025-03-28 at 11 09 56 AM" src="https://github.com/user-attachments/assets/be3277d0-45e5-428b-bd29-d7a70e2860b1" />

## How to #Synchronize (ThreadSafe) ArrayList in Java

<img width="693" alt="Screenshot 2025-03-28 at 9 57 21 AM" src="https://github.com/user-attachments/assets/0500de1b-3a49-46e5-a2ea-a85c7bffb1c3" />
<img width="949" alt="Screenshot 2025-03-28 at 10 25 00 AM" src="https://github.com/user-attachments/assets/cdbe5ec4-6f01-4136-9cc3-1e6a3b1efedf" />
<img width="910" alt="Screenshot 2025-03-28 at 10 32 32 AM" src="https://github.com/user-attachments/assets/b907d58b-a9b9-4e98-aec6-c65b515926a2" />
 
### ✅ **Key Takeaways About `CopyOnWriteArrayList`**
1. **It is thread-safe** → No `ConcurrentModificationException`, even if multiple threads modify the list at the same time.  
2. **It uses a copy-on-write mechanism** → Every modification (add, remove, set) creates a **new copy of the list**.  
3. **Iterators see a snapshot of the list** → This means:
   - **Reads are consistent but may be stale.**  
   - **Writes do not affect existing iterators.**  
   - **Different threads might see different versions of the list.**  

### 💡 **Real-World Example**
Imagine an **e-commerce app** where multiple users check the list of products:  
- If an admin **removes a product**, some users might **still see the old product list** (because they are using an older snapshot).  
- This is **not a real-time list**—it’s **eventually consistent**.  

---

### 🔥 **Is `CopyOnWriteArrayList` the Right Choice for Your Use Case?**
| Use Case | Should You Use `CopyOnWriteArrayList`? | Alternative |
|----------|--------------------------------|-------------|
| **Frequent reads, few writes** (e.g., product catalog, user roles) | ✅ YES (Good for read-heavy applications) | - |
| **Frequent modifications (many writes)** | ❌ NO (Expensive due to list copying) | `synchronized List` or `ConcurrentLinkedQueue` |
| **Real-time consistency needed** (e.g., stock trading app, financial transactions) | ❌ NO (Threads may see stale data) | `synchronized List`, `ReentrantLock`, `BlockingQueue` |

---

### 🚀 **Final Answer**
✔ **`CopyOnWriteArrayList` is great when you need thread safety but can tolerate slightly outdated data.**  
❌ **If real-time consistency is critical, use `synchronized List` or `ReentrantLock`.**  

