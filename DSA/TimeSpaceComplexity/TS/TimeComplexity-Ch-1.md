## What is Time Complexity?

Consider an old computer and a M1 Macbook. Suppose there are 10,00,000 elements in an array & we try to do a linear search for a number that doesn't exist in the array. The old computer takes 10 secs of time while Macbook takes 1 sec of time.

#### Which one has a better Time Complexity?
None. Both of these machines have the same Time Complexity.

<img width="1026" alt="Screenshot 2024-07-04 at 8 24 29 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/dffe35dd-d344-4865-a0e9-929a8119df7f">

These are straight lines. The only difference is the slope is reduced in the second case. So, we can conclude that even though the time taken is different, but the relationship between the size and the time is the same (linear).

## Takeaway
- Time Complexity is not equal to time taken.
- TimeComplexity is a Mathematical function that tells us how Time grows as the Input grows

## Why is this Relationship important?

If we fix the size of larger numbers, we can observe that the time taken by linear search is greater than the time taken by binary search.
We can conclude that O(log n) is better. 

<img width="950" alt="Screenshot 2024-07-04 at 8 31 34 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/566b5477-b7b2-46fc-9e21-9ca5c4f07ec6">

Constant time complexity is even better than both of these.

<img width="1009" alt="Screenshot 2024-07-04 at 8 34 34 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/eaff9f3f-bc60-4a5b-8f87-5de31b7b7bd6">

```
So, O(1) < O(log n) < O(n)
```

This is the reason why Binary Search is better.

## What do we consider when thinking about Complexity?

- Always look for the Worst Case Complexity
- Always look at Complexity for large infinite data
- Consider the below graph

  <img width="922" alt="Screenshot 2024-07-04 at 8 40 55 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/19469882-f095-48fc-a9ea-f3ac0aac4af9">

  - We can observe that, although being linear, the actual value is different for all. However, we cannot deny that even though the values      of the actual time are different, they are all growing linearly
  - We don't care about what the actual time is as it varies from machine to machine
  - Even though it gives us the time precisely, we don't really need the correct time. Rather we need the Relationship.
  - This is why, we ignore all Constants
- Always ignore less dominant terms.

  Consider the time complexity O(n^3 + log n)

  <img width="1006" alt="Screenshot 2024-07-04 at 8 51 31 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9caa5777-e995-41b4-8736-b91bd24bce76">

  Suppose the total Time taken is *(1 mill) ^ 3 secs* + *6 secs*.

  Does 6 secs have any significance compared to (1 mill) ^ 3 secs? - **NOT REALLY**

  <img width="984" alt="Screenshot 2024-07-04 at 8 53 26 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a248700e-5b30-45a9-bc96-1034ffd44752">
  
  ## O(1) < O(log n) < O(n) < O(2^n)
  Note: there are multiple other time complexities like O(n^2), O(n long), etc which will lie somewhat in between.

# Big-O Notation

Suppose we say that an algorithm has a complexity of O(N^3). In simple language, it means that it is the upper bound. The Complexity/relationship cannot exceed N^3. It may be solved in less time but won't even exceed N^3.

### Mathematical Representation

f(n) = O(g(n))

<img width="985" alt="Screenshot 2024-07-04 at 8 59 35 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8c473b65-f83f-4c7f-b068-39926c5d8713">

Consider an example,

<img width="1013" alt="Screenshot 2024-07-04 at 9 02 12 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/aa7aa769-46d3-4330-8d34-ca4022b9c045">
<img width="1012" alt="Screenshot 2024-07-04 at 9 02 20 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/759a4310-5d9b-4019-ac8b-b490d8cd8b91">

# Big Omega Notation

This represents Lower Bound. Minimum time Complexity required.

<img width="999" alt="Screenshot 2024-07-04 at 9 05 36 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/19ca0354-6ac4-44b4-a0bf-7684d3f3094e">

# Theta Notation

#### What if an algorithm has a lower bound and an upper bound as n^2?

We can represent it using Theta Notation.

<img width="1008" alt="Screenshot 2024-07-04 at 9 09 35 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7ac76c5f-ae97-4921-aac0-1cf9697fd7c6">

# Little o Notation

<img width="1014" alt="Screenshot 2024-07-04 at 9 10 15 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/6f112426-1985-47aa-aacc-a0eb5bdb03dc">
<img width="1015" alt="Screenshot 2024-07-04 at 9 10 32 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/e1d3608a-a6b9-4ca4-8e41-a918f3423a64">

# Little omega Notation

<img width="1017" alt="Screenshot 2024-07-04 at 9 11 11 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/6135d159-e736-4385-823e-7603bd6cbc7a">
<img width="1018" alt="Screenshot 2024-07-04 at 9 11 18 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/4769e0b6-412b-4a49-93bc-d43d00789d7e">


