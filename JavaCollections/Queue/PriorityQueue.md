## **Priority Queue in Java**
A **Priority Queue** is a data structure similar to a queue, but with a key difference: **elements are dequeued based on priority rather than the order of insertion**. In Java, the `PriorityQueue` class, part of the `java.util` package, implements this structure.

---

## **Characteristics of a Priority Queue**
1. **Ordering**: Elements are **ordered based on their priority**, which by default follows the **natural ordering (min-heap)**.
2. **Heap Implementation**: Java’s `PriorityQueue` is implemented using a **binary heap** (a complete binary tree), making insertion and deletion efficient.
3. **Not Thread-Safe**: It is **not synchronized**. If multiple threads access it concurrently, you should use `PriorityBlockingQueue`.
4. **No Fixed Size**: It is **dynamically resizable**.
5. **Duplicates Allowed**: Unlike sets, **duplicate elements** can exist in a priority queue.

---

## **Constructors of PriorityQueue in Java**
```java
PriorityQueue<E> pq = new PriorityQueue<>();  // Default (Min-Heap)
PriorityQueue<E> pq = new PriorityQueue<>(int initialCapacity);
PriorityQueue<E> pq = new PriorityQueue<>(Comparator<? super E> comparator);
PriorityQueue<E> pq = new PriorityQueue<>(Collection<? extends E> c);
```

- **Default Constructor**: Implements a **Min-Heap** (smallest element has the highest priority).
- **With Comparator**: Allows custom ordering (e.g., Max-Heap).
- **With Collection**: Initializes from another collection.

---

## **Basic Operations**
| Operation | Method | Time Complexity |
|-----------|--------|----------------|
| Insert (Enqueue) | `add(E e)` / `offer(E e)` | O(log N) |
| Remove (Dequeue) | `poll()` | O(log N) |
| Get Top Element | `peek()` | O(1) |
| Check Size | `size()` | O(1) |
| Check If Empty | `isEmpty()` | O(1) |

---

## **Example: Min-Heap (Default)**
```java
import java.util.PriorityQueue;

public class MinHeapExample {
    public static void main(String[] args) {
        PriorityQueue<Integer> pq = new PriorityQueue<>();

        pq.add(10);
        pq.add(5);
        pq.add(20);
        pq.add(1);

        System.out.println(pq.poll()); // Output: 1 (smallest element)
        System.out.println(pq.poll()); // Output: 5
    }
}
```

---

## **Example: Max-Heap (Custom Comparator)**
```java
import java.util.PriorityQueue;
import java.util.Collections;

public class MaxHeapExample {
    public static void main(String[] args) {
        PriorityQueue<Integer> pq = new PriorityQueue<>(Collections.reverseOrder());

        pq.add(10);
        pq.add(5);
        pq.add(20);
        pq.add(1);

        System.out.println(pq.poll()); // Output: 20 (largest element)
        System.out.println(pq.poll()); // Output: 10
    }
}
```

---

## **PriorityQueue with Custom Objects**
```java
import java.util.*;

class Student {
    String name;
    int rank;

    public Student(String name, int rank) {
        this.name = name;
        this.rank = rank;
    }
}

class RankComparator implements Comparator<Student> {
    public int compare(Student s1, Student s2) {
        return s1.rank - s2.rank; // Ascending order (Min-Heap)
    }
}

public class CustomPQ {
    public static void main(String[] args) {
        PriorityQueue<Student> pq = new PriorityQueue<>(new RankComparator());

        pq.add(new Student("Alice", 2));
        pq.add(new Student("Bob", 1));
        pq.add(new Student("Charlie", 3));

        System.out.println(pq.poll().name); // Output: Bob (lowest rank)
    }
}
```

---

## **Common Interview Questions on PriorityQueue**
### **1. Find the Kth Largest Element in an Array**
- **Approach**: Use a **Min-Heap of size K**.
```java
import java.util.PriorityQueue;

public class KthLargestElement {
    public static int findKthLargest(int[] nums, int k) {
        PriorityQueue<Integer> pq = new PriorityQueue<>(); // Min-Heap

        for (int num : nums) {
            pq.offer(num);
            if (pq.size() > k) {
                pq.poll(); // Remove smallest element
            }
        }
        return pq.peek();
    }

    public static void main(String[] args) {
        int[] nums = {3, 2, 1, 5, 6, 4};
        System.out.println(findKthLargest(nums, 2)); // Output: 5
    }
}
```

---

### **2. Merge K Sorted Lists**
- **Approach**: Use a **Min-Heap** to always poll the smallest element.
```java
import java.util.PriorityQueue;

class ListNode {
    int val;
    ListNode next;

    ListNode(int val) {
        this.val = val;
        this.next = null;
    }
}

public class MergeKSortedLists {
    public ListNode mergeKLists(ListNode[] lists) {
        PriorityQueue<ListNode> pq = new PriorityQueue<>((a, b) -> a.val - b.val);

        for (ListNode node : lists) {
            if (node != null) pq.offer(node);
        }

        ListNode dummy = new ListNode(-1), current = dummy;

        while (!pq.isEmpty()) {
            ListNode smallest = pq.poll();
            current.next = smallest;
            current = smallest;

            if (smallest.next != null) {
                pq.offer(smallest.next);
            }
        }
        return dummy.next;
    }
}
```

---

### **3. Top K Frequent Elements**
- **Approach**: Use a **Min-Heap** to keep track of K most frequent elements.
```java
import java.util.*;

public class TopKFrequentElements {
    public static List<Integer> topKFrequent(int[] nums, int k) {
        Map<Integer, Integer> freqMap = new HashMap<>();
        for (int num : nums) {
            freqMap.put(num, freqMap.getOrDefault(num, 0) + 1);
        }

        PriorityQueue<Integer> pq = new PriorityQueue<>((a, b) -> freqMap.get(a) - freqMap.get(b));

        for (int num : freqMap.keySet()) {
            pq.offer(num);
            if (pq.size() > k) {
                pq.poll();
            }
        }

        List<Integer> result = new ArrayList<>();
        while (!pq.isEmpty()) {
            result.add(pq.poll());
        }
        Collections.reverse(result);
        return result;
    }

    public static void main(String[] args) {
        int[] nums = {1, 1, 1, 2, 2, 3};
        System.out.println(topKFrequent(nums, 2)); // Output: [1, 2]
    }
}
```

---

### **Other Interview Questions**
1. **Implement a Median Finder** using two heaps (Max-Heap and Min-Heap).
2. **Find the K closest points to the origin** using a Max-Heap.
3. **Merge K sorted arrays** using a Min-Heap.
4. **Rearrange characters in a string** so that no two adjacent are the same (Greedy + Heap).
5. **Task Scheduler**: Schedule tasks with cool-down periods (Greedy + PriorityQueue).

---

## **Key Takeaways**
- Java’s `PriorityQueue` is based on **binary heap**.
- By default, it is a **Min-Heap**; use a **custom comparator** for Max-Heap.
- It allows **duplicate values** and **does not support null values**.
- **Time Complexity**:
  - **Insertion & Removal**: `O(log N)`
  - **Peek (Get top element)**: `O(1)`

