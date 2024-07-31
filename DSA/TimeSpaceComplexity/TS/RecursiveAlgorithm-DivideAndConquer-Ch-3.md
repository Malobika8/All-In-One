## Recursive Algorithms

In this case, time needs to be considered for every single function call.

Space Complexity: Recursive programs do not have constant Space Complexity. This is because the function calls are stored in Stack and 
hence takes memory.

Note: Only calls that are interlinked with each other will be called at the same time.

<img width="1021" alt="Screenshot 2024-07-04 at 3 27 26 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/93e4083b-6fb2-4ccf-a9d7-a44c820b99a3">

```
The longest chain from root to leaf of the Recursion tree determines Space complexity.
Space Complexity = HeightPath of the Tree = total number of elements present in the program = O(n)
```

#### Types of Recursion problems:
- Linear: f(n) = f(n-1) + f(n-2)
- Divide & Conquer: f(n) = f(n/2) + O(1)

### Divide & Conquer Recurrence Relations

Form of Divide and Conquer Recurrence: 

(Note that these are all "x" (might look confusing))

<img width="1024" alt="Screenshot 2024-07-31 at 1 11 34 PM" src="https://github.com/user-attachments/assets/c9f92f19-263d-4226-8ac5-ffa18a3d18b1">

Example 1:

<img width="1007" alt="Screenshot 2024-07-31 at 1 16 41 PM" src="https://github.com/user-attachments/assets/135c0feb-4afc-4cfe-bf2e-93516949f9d5">

Example 2:

<img width="1001" alt="Screenshot 2024-07-31 at 1 16 48 PM" src="https://github.com/user-attachments/assets/e6e42312-5ddf-4858-9934-bd1a6c54c74e">

Example 3: Consider Merge Sort. 
- Sort the first half of the array.
- Sort the second half of the array.
- Merge the two sorted halves.

<img width="1006" alt="Screenshot 2024-07-31 at 1 17 09 PM" src="https://github.com/user-attachments/assets/ce53004f-1a44-4606-b23d-84a3fa617ee8">

g(n) basically denotes what we are doing with the segment i.e. merging the 2 sorted halves (n-1).

## How to solve these recurrence relations to get complexity? How can we get the Time Complexity i.e. Big O notation formulas of these equations?

There are a few ways:
- Plug & Chug: Take the formula, put values, and keep going.
- Master's Theorem.
- Akra Bazzi (1996):

  ### Solve Divide & Conquer Recurrence Relation
  
  <img width="1011" alt="Screenshot 2024-07-31 at 1 39 20 PM" src="https://github.com/user-attachments/assets/a4f231dc-6d7f-4578-82f2-742348738d57">

  We would need to do basic integration.

  <img width="569" alt="Screenshot 2024-07-31 at 1 40 51 PM" src="https://github.com/user-attachments/assets/5c5f4ee5-e6a8-4765-83f3-bad79a316ed3">

  ---------------------------------------
  #### Why do we write constants as O(1)?

  This is because any constant value can considered as the value itself multiple by 1. So, we can ignore
  the value & just write O(1).

  <img width="298" alt="Screenshot 2024-07-31 at 1 42 32 PM" src="https://github.com/user-attachments/assets/f365f03f-b83d-4748-ac83-b19cd783cd06">
  
  ---------------------------------------

  ### Q1. Let's consider Merge Sort example & find the complexity using the "*Akra Bazzi*" formula.

  <img width="733" alt="Screenshot 2024-07-31 at 1 45 45 PM" src="https://github.com/user-attachments/assets/c7f41de2-74c4-4ed4-9ffe-b5686674474e">

  Once we find "p", put it in the "*Akra Bazzi*" formula.

  <img width="1020" alt="Screenshot 2024-07-31 at 1 46 19 PM" src="https://github.com/user-attachments/assets/3304e095-eb1b-4ffb-9aab-f8d7df0ca5f3">
  <img width="1013" alt="Screenshot 2024-07-31 at 1 46 37 PM" src="https://github.com/user-attachments/assets/9813e1f1-c971-4e0b-a2ac-f5e68ae2cf6b">
  <img width="1015" alt="Screenshot 2024-07-31 at 1 46 46 PM" src="https://github.com/user-attachments/assets/80f87387-3ed8-4c02-80ef-8c14c29145eb">

  ### Q2. Let's see another example.

  <img width="1020" alt="Screenshot 2024-07-31 at 1 54 33 PM" src="https://github.com/user-attachments/assets/b8bbabfa-1635-4c31-9263-cf9c1e0ef765">
  <img width="1020" alt="Screenshot 2024-07-31 at 1 54 41 PM" src="https://github.com/user-attachments/assets/a76a889d-e24a-469e-b78e-b05301870785">

  ### What if we can't find the value of "p"?

  <img width="1015" alt="Screenshot 2024-07-31 at 2 00 31 PM" src="https://github.com/user-attachments/assets/250b9b55-d0dd-4e2f-8cd8-f7d99f3ad0da">
  <img width="1020" alt="Screenshot 2024-07-31 at 2 00 41 PM" src="https://github.com/user-attachments/assets/eb4b1bab-71e7-4f48-b3bb-abefbec4dffb">

  ```
  When p is less than power of g(x), ans = O(g(x))
  ```
  
  <img width="1017" alt="Screenshot 2024-07-31 at 2 00 53 PM" src="https://github.com/user-attachments/assets/de481a95-7234-453b-a4f3-3392032e87f9">

  #### Why though?

  <img width="1022" alt="Screenshot 2024-07-31 at 2 59 13 PM" src="https://github.com/user-attachments/assets/1b1b92a2-04cf-4664-a07d-bcad91901c8a">
  


  
















