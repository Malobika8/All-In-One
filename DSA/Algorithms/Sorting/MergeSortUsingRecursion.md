# Merge Sort

### Steps:
1. Divide array into 2 parts
2. get both parts sorted via Recursion
3. When we get the sorted parts, merge them

Flow of execution,

<img width="1024" alt="Screenshot 2024-08-08 at 9 08 14 PM" src="https://github.com/user-attachments/assets/f2edb122-df1f-4084-9a7b-7327c75b05f7">

Merge logic

<img width="941" alt="Screenshot 2024-08-08 at 9 08 38 PM" src="https://github.com/user-attachments/assets/3c9565a3-9160-4f2b-ac30-3f4f2cddc022">

Divide the arrays and sort

<img width="941" alt="Screenshot 2024-08-08 at 9 08 32 PM" src="https://github.com/user-attachments/assets/7d55abe2-cce2-4dff-8556-1697a622e28a">

Main method

<img width="959" alt="Screenshot 2024-08-08 at 9 08 26 PM" src="https://github.com/user-attachments/assets/516b9cdd-41bf-48ce-bdff-4fbee9b6c5f1">

## Time Complexity

At every level, n elements are being merged.

<img width="1024" alt="Screenshot 2024-08-08 at 9 14 19 PM" src="https://github.com/user-attachments/assets/9f0c5e23-c7e8-4c79-8b76-71475a452d8e">

So, total comparisions made: n

Divisions happen at every level. Let total number of levels be k, the no of division will be n/2^k which is nothing but 1.

<img width="1016" alt="Screenshot 2024-08-08 at 9 18 23 PM" src="https://github.com/user-attachments/assets/268f7d3e-e9fb-4c87-bb21-6938c1916fc0">

We can take log of both & we'll get O(nLogn) as time complexity.

<img width="1019" alt="Screenshot 2024-08-08 at 9 18 31 PM" src="https://github.com/user-attachments/assets/1fd463ec-6cd8-4dfc-877f-3b441e44270c">

## Space Complexity

It is the maximum height of the tree. At one point of time, there will be total n elements in the stack together. Hence, it will be O(n).

# Let's try to find complexity with "Akra Bazzi formula"

There will be N/2 + N/2 division & total (n-1) comparisions while merging.

Ther Recurrence relation will be,

<img width="1020" alt="Screenshot 2024-08-08 at 9 27 32 PM" src="https://github.com/user-attachments/assets/3be71d40-cc40-4bc0-81ab-fb929f6ad78f">
<img width="1021" alt="Screenshot 2024-08-08 at 9 27 42 PM" src="https://github.com/user-attachments/assets/0c4b1797-7766-4e5e-8507-d1d06fd027ce">

Putting the value,

<img width="1016" alt="Screenshot 2024-08-08 at 9 28 22 PM" src="https://github.com/user-attachments/assets/86558c94-6d4a-4c92-9087-953850311dd5">

# In-place algorithm

Instead of making a copy of the array and sending to function call, we can pass index of array.

<img width="1008" alt="Screenshot 2024-08-08 at 9 33 13 PM" src="https://github.com/user-attachments/assets/a901038b-46d5-4850-a079-20acf2ba13fd">
<img width="996" alt="Screenshot 2024-08-08 at 9 48 39 PM" src="https://github.com/user-attachments/assets/3fc666e9-c4af-4c0e-88ca-47520d6bd3be">
<img width="987" alt="Screenshot 2024-08-08 at 9 48 52 PM" src="https://github.com/user-attachments/assets/750e109d-f3da-44f6-a05d-54726256d3e1">








