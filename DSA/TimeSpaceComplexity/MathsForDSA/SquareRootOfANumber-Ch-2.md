# Ways to find square root of a number

## 1st method
### For perfect square roots
We can simply check if "*a*a == n*" (where a<n and n is the no whose square root we are trying to find). We can start from 1 and keep checking.

```
for(i=0;i*i<=n;i++)
```

We observe that the numbers are increasing & sorted. This means we can apply Binary search.

<img width="758" alt="Screenshot 2024-08-06 at 10 26 21 AM" src="https://github.com/user-attachments/assets/89b92313-4cf2-4c7d-99b8-825a4ed66081">

----------------

### For rest of the number, how do we get precision?

<img width="974" alt="Screenshot 2024-08-06 at 10 31 04 AM" src="https://github.com/user-attachments/assets/ffcb9db2-2915-4ba4-a175-fa9749f29a09">

Suppose we try to find the square root of 40. (It is 6.32)

Through Binary Search, we will find that "* 6*6=36 < 40 < 7*7=49 *". Once we reach that point, we can increment by 0.1. We can check if 
"* 6.1*6.1 < 40 *". If no, we can further increment by 0.1 and continue checking the same.

<img width="767" alt="Screenshot 2024-08-06 at 10 33 15 AM" src="https://github.com/user-attachments/assets/246422f8-71d7-4b3e-88a0-84956adb0ecd">

If we want precision by two digits, we can use the same strategy. This time we can increment by 0.01.

### Total time complexity will be approximately log(n).

### Code

<img width="458" alt="Screenshot 2024-08-06 at 10 43 14 AM" src="https://github.com/user-attachments/assets/f0d48fd4-a1be-4498-8b75-e09ad3ffd9b0">
<img width="452" alt="Screenshot 2024-08-06 at 10 42 49 AM" src="https://github.com/user-attachments/assets/7ad1e90e-de7f-4087-8e04-d27641e9c471">
<img width="751" alt="Screenshot 2024-08-06 at 10 39 19 AM" src="https://github.com/user-attachments/assets/444ba038-30c6-4ecf-8b58-fbb660ba7700">

## 2nd method - Newton Raphson(Square root) Method

It says that the formula for Newton Raphson method is,

<img width="1013" alt="Screenshot 2024-08-06 at 10 48 51 AM" src="https://github.com/user-attachments/assets/ca0d880e-1927-4d39-99ca-ec46836cbc3e">

where "X" is the square root we assumed.

#### Why is it working though?

We can actually confirm that if we make the correct guess, LHS will be equal to RHS (i.e. the equation satisfies).

<img width="1136" alt="Screenshot 2024-08-06 at 12 34 10 PM" src="https://github.com/user-attachments/assets/551b3439-1b69-44ff-9d63-3e7cf3b40a30">

Difference between whatever root we find from the above formula & the root that we guessed, is basically error.

<img width="1019" alt="Screenshot 2024-08-06 at 12 32 53 PM" src="https://github.com/user-attachments/assets/6eac8082-ba83-4bfd-a882-622edd6056b3">

As we lower the error, we get more precise answer. But, the number of iterations will increase. We can minimize the error as much as possible.

<img width="480" alt="Screenshot 2024-08-06 at 12 29 55 PM" src="https://github.com/user-attachments/assets/fea50a55-bfe5-4219-b2e8-e47ec3a00d1e">



















