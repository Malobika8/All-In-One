# Questions:

### Important points;
- Applicable to all binary numbers: All digits are power of 2 except the last digit of every Binary Number
- The rightmost digit/last digit is known as LSB (least significant digit)
- n & 1 == 1

  We can use this to find if a number is even/odd.
  
  Explanation: If the rightmost bit is 1, number is odd. This is because 2^0 is 1. So whether the number is even or odd entirely depends upon
  the rightmost bit.

  If the rightmost bit is 0, number is even.

  <img width="995" alt="Screenshot 2024-07-07 at 10 04 02 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/448951bc-cacf-411a-8ef4-00ada6c5d6e2">

- Every number is calculated in binary form internally.
- Bitwise Operators also follow associative properties.
  
#### Q1. Given a number, n, find if it is odd or even.

- If we add any number with 1, it gives the same number.
- If we add any number with 0, it results to 0.
- To find the last digit:
  - Do AND of last digit with 1
  - Do AND of every other digit with 0

    Example:
 
    100101 & 000001 = 000001

    The number is odd since the last digit(rightmost digit) is 1.
    
<img width="1013" alt="Screenshot 2024-07-07 at 10 04 48 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8a04ee55-7545-440a-b109-df6379da3859">
<img width="851" alt="Screenshot 2024-07-07 at 10 12 23 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/cfef3227-de2b-45fc-9f1e-1f52670f47ff">

#### Q2. Given an array of numbers, find the unique element.

We know 2 things.
- Any number XOR with itself gives 0.
- 0 XOR with any number gives the number itself
- The mathematical operators follow associative property (order doesn't matter) i.e. (2^2) ^ (7^7) ^ 6 == 6 == (2^7) ^ 6 ^ (7^2)

XOR all the numbers.

Time Complexity: O(n)
Space Complexity: O(1)

<img width="771" alt="Screenshot 2024-07-07 at 10 20 29 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c55eefa9-431a-4f8e-ab69-38fee14a3452">

#### Q3. Find the ith bit of a number.

We know that a number AND with 1 gives the number itself. So, we can do ith bit AND 1.

Ex: Position = 4, 

    1001100 AND (0001000 (masked))

    How do you find the masked number? - 1<<(i-1)

    So, result = number AND (1<<(i-1))

<img width="1025" alt="Screenshot 2024-07-08 at 9 30 55 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/61e02720-7657-43d4-a694-9fb1ee341f14">

#### Q4. Set the ith bit of a number.

We know that a number OR with 1 gives 1.

<img width="1021" alt="Screenshot 2024-07-08 at 9 31 06 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a773da10-c011-4527-ac22-7871154722ee">

#### Q5. Reset the ith bit of a number.

- number AND 0
- get the mask and complement it

<img width="1022" alt="Screenshot 2024-07-08 at 9 31 20 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/802cc20c-18b8-4740-9149-921d79efa066">

#### Q6. Find the position of the rightmost set bit.

