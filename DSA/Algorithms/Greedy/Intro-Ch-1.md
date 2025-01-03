# Let's understand greedy with the help of an example

The **Jump Game** problem is considered a greedy problem because it involves making locally optimal choices at each step to achieve a globally optimal solution. Here's why:

### Problem Description (Jump Game):
Given an array of non-negative integers, where each element represents the maximum number of steps you can jump forward from that position, determine whether you can reach the last index starting from the first index.

---

### Greedy Approach Explanation:

1. **Goal**: 
   The goal is to determine if the last index is reachable. To achieve this, we focus on tracking the **maximum reachable index** as we iterate through the array.

2. **Key Idea**:
   At each position, calculate the farthest index you can reach (i.e., `current index + jump length at that index`). Update the maximum reachable index based on this calculation.

3. **Greedy Choice**:
   The greedy approach works because:
   - At every index, you make the locally optimal choice of jumping as far as possible.
   - If, during this process, the maximum reachable index surpasses or reaches the last index, the last index is reachable.

4. **Termination**:
   - If at any point, the maximum reachable index is less than the current index, you can't proceed further, and the last index is not reachable.
   - Otherwise, if you finish iterating through the array and the maximum reachable index is greater than or equal to the last index, the last index is reachable.

---

### Example:

**Input**: `[2, 3, 1, 1, 4]`

1. Start at index 0 (value = 2), maximum reachable = 0 + 2 = 2.
2. At index 1 (value = 3), maximum reachable = max(2, 1 + 3) = 4.
3. At index 2 (value = 1), maximum reachable = max(4, 2 + 1) = 4.
4. At index 3 (value = 1), maximum reachable = max(4, 3 + 1) = 4.
5. At index 4, we have already reached the last index.

**Output**: `True` (We can reach the last index).

---

### Why is it Greedy?

The solution doesn't backtrack or explore all possible paths. Instead, it makes a single pass through the array, always choosing the farthest possible jump at each step to ensure the problem is solved efficiently. This greedy strategy ensures a time complexity of **O(n)**, which is optimal.


Let's analyze the array `[3, 2, 2, 0, 4]` using the **greedy approach** step by step to determine if we can reach the last index:

---

### Step-by-Step Analysis:

1. **Start at index 0 (value = 3):**
   - Maximum reachable index = `0 + 3 = 3`.

2. **Move to index 1 (value = 2):**
   - Maximum reachable index = `max(3, 1 + 2) = 3`.

3. **Move to index 2 (value = 2):**
   - Maximum reachable index = `max(3, 2 + 2) = 4`.

4. **Move to index 3 (value = 0):**
   - Maximum reachable index remains `4` (because `3 + 0 = 3 < 4`).

5. **Move to index 4:**
   - Index 4 is within the maximum reachable range (`4 >= 4`).

---

### Conclusion:

We can reach the last index. The output is **`True`**.
