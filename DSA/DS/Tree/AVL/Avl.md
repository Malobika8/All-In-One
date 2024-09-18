# Steps

- Insert the node (n) normally
- Start from node (n) and find the node that makes the tree unbalanced, bottom up
- Using one of the 4 rules, rotate

## Note: grandchild is always in the line of where the element was added

# 4 Rules

1. Left left case: Right rotate p

   <img width="1007" alt="Screenshot 2024-09-18 at 8 48 59 AM" src="https://github.com/user-attachments/assets/857d1d5a-8a05-4b9f-91af-3048e28f2485">

2. Left right case: Left rotate c -> Right rotate p

   <img width="1011" alt="Screenshot 2024-09-18 at 8 51 24 AM" src="https://github.com/user-attachments/assets/3c2083c2-9a96-416f-9fe6-3b8db606dfc2">

3. Right right case: Left rotate p

   <img width="1020" alt="Screenshot 2024-09-18 at 8 53 36 AM" src="https://github.com/user-attachments/assets/80d3673d-e1b7-49d8-bfea-bbbe97910073">

4. Right left case: Right rotate c -> Left rotate p

   <img width="1020" alt="Screenshot 2024-09-18 at 8 56 11 AM" src="https://github.com/user-attachments/assets/4412c4d6-46ba-4dea-9a17-6930a3b416f7">


   
