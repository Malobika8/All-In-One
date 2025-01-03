# Dynamic Programming

## Two ways:

- ### Recursion + Memoization:

  Simple recursion but with data stored which is used later, whenever required, instead of computing the same thing again.

  Recursion should be done taking memoization into account. It should be designed in such a way that previous computations can be used.

  #### Consider fibonacci series

  - Plain recursive way: This is not designed for memorization.

    <img width="502" alt="Screenshot 2025-01-03 at 6 53 28 PM" src="https://github.com/user-attachments/assets/e9c7f80f-8eb2-4668-8ca3-3e7d17a4482b" />

  - Recursion designed for memorization: Previously computed values can be used later.

    <img width="944" alt="Screenshot 2025-01-03 at 6 55 42 PM" src="https://github.com/user-attachments/assets/ee3a5b65-1d5a-43c0-9ac4-b8453755a5b2" />
  
- ### Tabulation method:

  Data is stored in a table by comparing it with previously stored values.
