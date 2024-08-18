## Subsets

<img width="1015" alt="Screenshot 2024-08-17 at 11 33 11 AM" src="https://github.com/user-attachments/assets/3119e11e-894c-4749-a8ec-63d35ba5017e">

### Q1. Create all the subsets of a list

<img width="1004" alt="Screenshot 2024-08-17 at 11 35 39 AM" src="https://github.com/user-attachments/assets/d3e30869-acd4-4123-87a0-2aa1755ab2c5">
<img width="1002" alt="Screenshot 2024-08-17 at 11 35 34 AM" src="https://github.com/user-attachments/assets/f684e04f-8480-435d-a981-9e0f5d4019f3">

#### Subset Pattern: 
Either we take it or we don't take it. The left side is finished first and then goes to the tree's right side.

<img width="1003" alt="Screenshot 2024-08-17 at 11 39 20 AM" src="https://github.com/user-attachments/assets/c6f7a9a7-874a-4138-9f62-958c598572e1">

<img width="995" alt="Screenshot 2024-08-17 at 11 45 53 AM" src="https://github.com/user-attachments/assets/e0dd08f3-8f6a-4df4-84f9-d17cc635e671">

Return a list

<img width="954" alt="Screenshot 2024-08-17 at 11 48 00 AM" src="https://github.com/user-attachments/assets/2e3696a4-a4be-48af-a6bd-5fa4b9070400">

OR

<img width="823" alt="Screenshot 2024-08-17 at 12 02 03 PM" src="https://github.com/user-attachments/assets/1559d8ed-2172-4011-8273-8cfec6c8b18f">

## How to do the same with Iteration?

We can either accept or reject

<img width="892" alt="Screenshot 2024-08-17 at 6 11 51 PM" src="https://github.com/user-attachments/assets/f8ad28e1-3c5b-4369-bc6b-e002baab4457">
<img width="1169" alt="Screenshot 2024-08-17 at 6 15 53 PM" src="https://github.com/user-attachments/assets/fde8e722-3aa2-4885-b87b-cd90abe2068f">

We can have a List of List. Initially, the list will be copied, and then a new element will be added to each sub-list.

<img width="952" alt="Screenshot 2024-08-17 at 6 17 15 PM" src="https://github.com/user-attachments/assets/b9e62454-0e41-43af-809c-a6dc905b05f1">

- Create a list of list
- Add an empty list
- Take one element from the num list
- Iterate through the outer list
  - Create a new list and copy ith the inner list
  - Add the element to the inner list
  - Add this new inner list to the outer list

### Time & Space Complexity

Total no of elements: n, Total no of subsets: 2^n

So, Time Complexity: O(n*2^n)

Space Complexity: O(2^n * n) i.e. Total subsets * space taken by each of the subsets

### What if we have duplicate elements i.e. [1, 2, 2]?

- When you find a duplicate element, only add it to the newly created subset of the previous step.
- Array should be sorted
  
<img width="1019" alt="Screenshot 2024-08-18 at 11 37 02 AM" src="https://github.com/user-attachments/assets/e77f4577-9914-45d5-b112-f2086296b9da">
<img width="974" alt="Screenshot 2024-08-18 at 12 13 17 PM" src="https://github.com/user-attachments/assets/2f1329a6-2566-43f4-9a51-8eefffc9ba9d">




