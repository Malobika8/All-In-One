# Insertion Sort

Insertion sort is a simple sorting algorithm that works by iteratively inserting each element of an unsorted list into its correct position in a sorted portion of the list. It is a stable sorting algorithm, meaning that elements with equal values maintain their relative order in the sorted output.
Insertion sort is like sorting playing cards in your hands. You split the cards into two groups: the sorted cards and the unsorted cards. Then, you pick a card from the unsorted group and put it in the right place in the sorted group.

### Insertion Sort Algorithm:
Insertion sort is a simple sorting algorithm that works by building a sorted array one element at a time. It is considered an “in-place” sorting algorithm, meaning it doesn’t require any additional memory space beyond the original array.

* ### Algorithm:
  
  To achieve insertion sort, follow these steps:
    - We have to start with second element of the array as first element in the array is assumed to be sorted.
    - Compare second element with the first element and check if the second element is smaller then swap them.
    - Move to the third element and compare it with the second element, then the first element and swap as necessary to put it in the correct position among the first three elements.
    - Continue this process, comparing each element with the ones before it and swapping as needed to place it in the correct position among the sorted elements.
    - Repeat until the entire array is sorted.

  **Time Complexity of Insertion Sort**
    - Best case: O(n), If the list is already sorted, where n is the number of elements in the list.
    - Average case: O(n2), If the list is randomly ordered
    - Worst case: O(n2), If the list is in reverse order
  **Space Complexity of Insertion Sort**
    - Auxiliary Space: O(1), Insertion sort requires O(1) additional space, making it a space-efficient sorting algorithm.
      
      ![image](https://github.com/Malobika8/GitDemo/assets/111234135/57700b46-21f4-4ded-8fed-5116a420434c)

      <img width="697" alt="Screenshot 2024-06-28 at 9 42 40 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/bbad67d2-6a92-44e7-92d3-874bea26370c">

      Input: [3, 7, 2, 1, 8]
      Output: [1, 2, 3, 7, 8]

 ### Why do we use?

  - It is adaptive. Steps gets reduced if sorted. No of swaps reduces as compared to Bubble sort.
  - It is stable
  - It is used for smaller values of N
  - Works good when array is partially sorted. This is why it takes part in hybrid sorting algorithms.
