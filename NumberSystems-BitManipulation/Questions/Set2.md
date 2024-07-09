## Q1. Find the unique element given that every number appears 3 times (or odd number of times) in an array of numbers.

<img width="1015" alt="Screenshot 2024-07-09 at 10 19 55 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8c7b3546-5106-4eb6-a71e-43cf2b905dda">
<img width="1013" alt="Screenshot 2024-07-09 at 10 20 06 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/580a2114-b871-49fa-8987-393e8409a9b6">

## Q2. Find the nth magic number

```
A magic number is defined as a number which can be expressed as a power of 5 or sum of unique powers of 5. First few magic numbers are
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

