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

    Since last digit(rightmost digit) is 1, number id odd.
    
<img width="1013" alt="Screenshot 2024-07-07 at 10 04 48 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8a04ee55-7545-440a-b109-df6379da3859">
<img width="851" alt="Screenshot 2024-07-07 at 10 12 23 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/cfef3227-de2b-45fc-9f1e-1f52670f47ff">

#### Q2. Given an array of numbers (every number appears twice), find the number that appears once.

Any number XOR with itself gives 0.

XOR all the numbers.

Time Complexity: O(n)
Space Complexity: O(1)

<img width="771" alt="Screenshot 2024-07-07 at 10 20 29 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c55eefa9-431a-4f8e-ab69-38fee14a3452">


