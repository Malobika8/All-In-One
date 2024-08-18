*The difference between Permutation and Combination is that for Permutation, the order of the members is taken into consideration but for 
Combination, orders of members does not matter.*

Consider the Recursion flow.

<img width="1326" alt="Screenshot 2024-08-18 at 1 32 44 PM" src="https://github.com/user-attachments/assets/1a2717fc-93b0-4b6d-b3aa-ef85ef91c4dc">

We can observe and devise formula to generate the unprocessed String (*up*).

```
up.substring(0,i)+up.substring(i+1, up.length()
```

<img width="965" alt="Screenshot 2024-08-18 at 1 34 15 PM" src="https://github.com/user-attachments/assets/ed2e9239-354a-49ad-b65a-d5486c0332c0">
<img width="1049" alt="Screenshot 2024-08-18 at 1 34 21 PM" src="https://github.com/user-attachments/assets/04e34d90-8c73-4afc-88d1-fe8804701472">
