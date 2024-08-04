## Q1. Find the unique element given that every number appears 3 times (or odd number of times) in an array of numbers.

<img width="1015" alt="Screenshot 2024-07-09 at 10 19 55 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8c7b3546-5106-4eb6-a71e-43cf2b905dda">
<img width="1013" alt="Screenshot 2024-07-09 at 10 20 06 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/580a2114-b871-49fa-8987-393e8409a9b6">

## Q2. Find the nth magic number (Amazon)

```
A magic number is defined as a number that can be expressed as a power of 5 or a sum of unique powers of 5. The first few magic numbers are
5, 25, 30(5 + 25), 125, 130(125 + 5), ….

Write a function to find the nth Magic number.
Example: 

Input: n = 2
Output: 25

Input: n = 5
Output: 130

If we notice carefully the magic numbers can be represented as 001, 010, 011, 100, 101, 110 etc, where 001 is 0*pow(5,3) + 0*pow(5,2) + 1*pow(5,1).
So basically we need to add powers of 5 for each bit set in a given integer n. 
```

<img width="1019" alt="Screenshot 2024-07-09 at 10 25 20 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9ef5a4e3-30cf-47ff-b594-8ed975e1f704">
<img width="1017" alt="Screenshot 2024-07-09 at 10 25 29 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/6e00fb49-cded-48ea-8123-8743b136a8d4">
<img width="809" alt="Screenshot 2024-07-09 at 10 25 06 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/5a682e7c-1c99-4298-9de5-ee8087540e61">

### Time Complexity = O(log n) 

#### This is because the loop runs (log n) times. See the next question for more clarity.

## Q3. Find the number of digits in base b. Ex: 2 in binary is 10. So, number of digits = 2

- One way would be to keep and counter and do a right shift till we get 0.
- Second is by deriving a formula.

  We know that,

  <img width="978" alt="Screenshot 2024-08-02 at 8 54 00 PM" src="https://github.com/user-attachments/assets/8d9079af-64b0-4d10-a8a6-06a64f44a4f3">

  (how many times b is multiplied to get a)

  Here, x is the representation of the base.

  <img width="774" alt="Screenshot 2024-08-02 at 8 57 10 PM" src="https://github.com/user-attachments/assets/8b4df4c8-1bec-419e-bafd-442700728a02">

  Example:

  <img width="1019" alt="Screenshot 2024-08-02 at 9 01 34 PM" src="https://github.com/user-attachments/assets/cfd6dbca-d38a-4921-a54c-32d0fbc49d94">

  This means "how many times 2 has been multiplied to form 10".

  Formula:

  <img width="1020" alt="Screenshot 2024-08-02 at 9 02 37 PM" src="https://github.com/user-attachments/assets/581880a8-5a00-40b1-b589-79945d8ef67f">

  Code:

  <img width="777" alt="Screenshot 2024-08-02 at 9 04 57 PM" src="https://github.com/user-attachments/assets/a98f86d1-02fd-4ed5-8581-efce90364996">

  Note that,

  <img width="1041" alt="Screenshot 2024-08-02 at 9 07 16 PM" src="https://github.com/user-attachments/assets/fc808ff9-e878-4a9a-8179-519e3b0634d5">


## Q4. Find the sum of nth row of Pascal's triangle.

Pascal's triangle:

<img width="436" alt="Screenshot 2024-08-02 at 9 17 24 PM" src="https://github.com/user-attachments/assets/5ab846a9-c365-4273-8b31-e66e46b152e5">
<img width="1127" alt="Screenshot 2024-08-02 at 9 17 37 PM" src="https://github.com/user-attachments/assets/55d93ee9-f58c-45dc-a77e-003a17689664">
<img width="980" alt="Screenshot 2024-08-02 at 9 18 28 PM" src="https://github.com/user-attachments/assets/b436e9dc-3057-46fc-838b-0deb8868dc98">

Idea:

<img width="1003" alt="Screenshot 2024-08-02 at 9 24 13 PM" src="https://github.com/user-attachments/assets/1bfb247d-751c-40cd-8bc4-387b67521678">

## Q5. Given a number, find out if it's a power of 2 or not.

There should be only one 1 and the rest of everything should be 0.

Example: 1000,100,1

Not a power of 2: 10010, 1010

- One way would be to right-shift the number and check if there's only one 1.
- We know that, 100000 = 1111 + 1

  4 in binary is 100 and 3 in binary is 11. So, we can write 4 = 3 + 1 i.e. 100 = 11 + 1.

  We can observe that,

  ```
  num(which is power of 2) & previous num = 0
  ```

  <img width="966" alt="Screenshot 2024-08-02 at 9 34 04 PM" src="https://github.com/user-attachments/assets/9aedfcaf-117d-4fc8-adb8-690086277c24">
  <img width="1041" alt="Screenshot 2024-08-02 at 9 35 32 PM" src="https://github.com/user-attachments/assets/ae8d256c-9079-43d9-8957-aa8d58337ab1">

  Code:

  <img width="784" alt="Screenshot 2024-08-02 at 9 36 35 PM" src="https://github.com/user-attachments/assets/79e91fe1-45cc-4ecb-919d-6a0da99a3cff">

  Note that 0 is an exception that we need to handle manually.

## Q6. Calculate a ^ b.

<img width="948" alt="Screenshot 2024-08-02 at 9 39 09 PM" src="https://github.com/user-attachments/assets/d7686965-3b75-4654-bbf4-06c629f56d2e">

We can think of "b" in terms of binary and then multiply the base with the answer whenever the last digit is 1. Note that with every iteration, the base should be multiplied by itself.

<img width="954" alt="Screenshot 2024-08-04 at 12 17 20 PM" src="https://github.com/user-attachments/assets/f1248e0a-d6e1-455f-995a-6c9d17f9b7b1">

## Q7. Given a number n, find the number of set bits in it.

- One way is to find the last digit and check if it's 1. Right shift at every iteration.
- 



  
  





  

  

  

