# Cycle Sort

### Pattern: When given numbers from range 1-N, use cyclic sort

Consider an Unsorted Array
```
3,5,3,1,4
```
### How do we sort this?

We can use *Bubble sort*, *Insertion sort* or maybe *Selection sort*. But it does in O(n^2) Time Complexity.

### What if we want to solve it in 1 single pass (n comparisions)? How to do cyclic sort?

Given that numbers are going to be from 1-N. Imagine when the array is sorted, all the no's are going to be at the correct indices.

We can infer that,

```
Index = Value - 1
```

<img width="1114" alt="Screenshot 2024-06-28 at 10 03 53 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d42916b2-cc16-4234-9149-070d0f63ac73">

* We can start from the very beginning. We will check if 3 is at the correct index. It ideally should be at 2(N-1).
* If yes, swap it with the correct index directly.
* If no, it means it is already at the correct index and we can move forward.
* We know the element we have swapped is in the correct position. But we are not sure if the other element with which it has been swapped is
  in the correct position or not.
* We will then check if he other element is at the correct index or not. If not we will swap it with the coorect index.

<img width="738" alt="Screenshot 2024-06-28 at 10 05 30 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/1c731716-1a33-4940-82b7-d59b136b947f">
<img width="582" alt="Screenshot 2024-06-28 at 10 06 41 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a031d1f3-50b9-44cf-b1c8-2fa5d3250aa2">
<img width="876" alt="Screenshot 2024-06-28 at 10 07 30 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/5a47d6f4-76b6-4f9a-a39d-6724ae5ff8a6">
<img width="608" alt="Screenshot 2024-06-28 at 10 08 16 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/3764023f-6b20-4f76-b904-0b3c418d592f">

Note: It is not required to increment "i" when we swap the elements. So, it might result in more number of Iterations of the loops.

### Worst Case:
  * Total N-1 no of Swaps are to take place.
  * For even correct Indices, we need to check if the element is in the correct index. So there will be total N no of Swaps.
  * Total swaps = (N-1) + N = 2N-1 = O(N)

## Code:
  
<img width="622" alt="Screenshot 2024-06-28 at 10 22 51 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/54bfc930-c824-4941-9a1e-a1fafc1f250b">

