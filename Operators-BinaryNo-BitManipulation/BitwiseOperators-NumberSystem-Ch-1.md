# Introduction

Internally everything is stored in 0's and 1's. 

### Note
- Base denotes how many numbers we have in that particular Number theory.
- Base2 Number System refers to Binary Number System which computer understands.
- 0 : false, 1 : true

## Bitwise Operators. 

1. Left Shift operator (<<): 

   - It shifts all the bits by 1 bit towards left
   - Extra 0 added to the right

   <img width="1005" alt="Screenshot 2024-07-07 at 9 14 06 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d1444a60-b68b-40e2-a671-4dd3b6cdb402">

   #### Observations:
   
   * Any number left shift by one gives double the number i.e. *A<<1 = A^2*
   * If we left shift A by B times, it's going to multiple A into 2^B i.e. *A<<B = A(2^B)*

     <img width="997" alt="Screenshot 2024-07-07 at 9 15 55 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8283f2f3-2461-4945-af57-9f6bcc956b18">

2. Right shift operator(>>):

   Shifts bits by 1 towards the right.

   <img width="1016" alt="Screenshot 2024-07-07 at 9 18 12 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/f04a4d43-e8b8-4792-aca7-14a6791cc71e">

   #### Observations:

   - *a>>b = a/(2^b)*

     <img width="1011" alt="Screenshot 2024-07-07 at 9 18 18 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/54d32d1c-9830-4e9c-a63d-da93cc1bea40">

   - Similar to decimal numbers, leading 0's are ignored. i.e. 00011100 = 11100

3. AND Operator:

   <img width="996" alt="Screenshot 2024-07-07 at 8 30 00 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/687b9ae2-206f-4bee-96cf-497112b39ddb">

   #### Observation:
   - Whenever we AND 1 with any number, digits remain the same.

     <img width="1017" alt="Screenshot 2024-07-07 at 8 31 58 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/e7e7e576-f98e-4a24-b617-bfe5b625b7b5">
  
4. OR Operator:

   If any one is true, entire expression is true.

   <img width="1018" alt="Screenshot 2024-07-07 at 8 32 27 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/eb61e49a-5ad2-413b-b67d-07008049679c">

5. XOR Operator:
   - If and only if
   - Exclusive if
   - If we have two numbers, only one of them should be true.

   <img width="1013" alt="Screenshot 2024-07-07 at 8 33 11 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/fac4e593-daf0-42dd-a17e-1bb35c2730ff">

   #### Observations:
   - XOR any number with 1 = Complement(opposite) of that number
   - XOR any number with 0 = Gives the number itself
   - XOR same number with same number = 0

   #### Complement :

   <img width="997" alt="Screenshot 2024-07-07 at 8 35 44 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9b7942ef-cd63-4639-9f69-fa4c3586984d">

## Number Systems

1. Decimal Number System: 0-9
   This is of base 10.
2. Binary numbers: 0,1
   This is of base 2.
3. Octal numbers: 0-7
   This is of base 8.

   *Example:*
   
   Decimal: 0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20
   
   Octal: 0,1,2,3,4,5,6,7,10,11,12,13,14,15,16,17,20,21,22,23.24

   We cannot use numbers that contain 8 and 9.

   So decimal equivalent of 9 is 11.

   9 base 10 = 11 base 8

   <img width="996" alt="Screenshot 2024-07-07 at 8 40 53 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/39cbbf31-2470-4832-b9a6-79804825a082">

4. Hexa decimal: This is used by a lot of computers.

   0-9 & a-f (16 in total)

   0,1,2,3,4,5,6,7,8,9,a,b,c,d,e,f

   10 in decimal = a in octal

   <img width="1013" alt="Screenshot 2024-07-07 at 8 37 31 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/5c86b51d-4561-4121-8e5c-d375405605ae">
   <img width="1014" alt="Screenshot 2024-07-07 at 8 43 23 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/498c4ee5-4925-44b2-8e41-3ca481dcf17b">

## Conversion into various Bases (Conversion to Number Systems)

1. Conversion from Decimal to base b:
   - Keep dividing by Base.
   - Take remainders and write it in opposite

     <img width="960" alt="Screenshot 2024-07-07 at 9 08 52 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/82ed4e46-7ac9-4696-869d-2489c1b9c502">

3. Conversion from Base b to Decimal:
   - Multiply and add the power of base with digits

     <img width="994" alt="Screenshot 2024-07-07 at 9 11 00 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/99e2bbbf-6881-4e3a-8fb7-c6b9d8ae0656">


### How to convert binary to octal?

- We can convert binary to decimal and then decimal to octal
