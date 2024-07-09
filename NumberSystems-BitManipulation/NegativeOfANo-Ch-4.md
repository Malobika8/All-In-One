# Complement of a number (Inversion)

To find the complement of a number, we can subtract the number from 1.

# Range of a number
   
   ```
   1 byte = 8 bits
   ```

   Most Significant bit tells us whether the number is positive or negative.

   #### 1=-ve and 0=+ve.

   If a number has more than 8 bits, the extra bits are not considered (they are discarded).

   If we calculate, total number of unique numbers (combinationation of 1's and 0's) would be 256 (-128(negative no's), 0 , 127(positive        no's).
   - 128 negative numbers.
   - 128 positive numbers(including 0)

   <img width="1017" alt="Screenshot 2024-07-09 at 8 57 34 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c012d038-1d2f-4506-890f-3db43c8ff214">
   <img width="1018" alt="Screenshot 2024-07-09 at 8 57 47 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/73287403-d790-42a3-a2e5-5a1f401c2495">

   ### Range Formula

   <img width="1019" alt="Screenshot 2024-07-09 at 8 57 58 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/66bb61fb-459d-4326-a59d-758b4aa6cf50">

# Negative of a number in Binary form.

   ### using 2's complement method
   Steps:
   - Take the complement of a number
   - Add 1 to it

   <img width="1020" alt="Screenshot 2024-07-09 at 8 39 53 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d3264b21-1eb7-404d-aca5-54059d56b0e1">
   <img width="1024" alt="Screenshot 2024-07-09 at 8 40 06 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/5e6a25dc-df6b-471c-bced-98d46d34f70b">

   #### Why though?

   Consider a number, 00001010. To find the complement of this number, we can subtract it from 0(i.e. 00000000). This is because a positive
   number when subtracted from 0 becomes a negative number.

   Now, we can write this as 100000000 instead as 00000000. This is because the first bit won't be considered as it is the 9th bit which is     more than 1 byte that is considered.

   Observe the following,

   * 8 in binary is 1000. This can be represented as 111 + 1 (which is 7+1 in decimal) (the sum is equal to 1000).
   * Similarly, 16 in binary is 10000. This can again be represented as 1111 + 1 (which is 15+1 in decimal)
  
   Coming back to our example, 100000000 can be represented as 11111111+1.

   So, 00000000 - 00001010 == 100000000 - 00001010 == 11111111 + 1 - 00001010 == (11111111 - 00001010) + 1

   From this, we can deduce the steps to find using 2's complement method.
   - Take the complement of a number (11111111 - 00001010). We can find complement by subtracting that number from 1.
   - Add 1 to it ((11111111 - 00001010) + 1)

   <img width="1018" alt="Screenshot 2024-07-09 at 8 56 42 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/cd1de8a1-6a05-4c8f-93db-4502071bf46f">
   <img width="1014" alt="Screenshot 2024-07-09 at 8 56 52 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/1fc88c32-a8bb-4bd8-9c89-8b4e5f14e640">


   



