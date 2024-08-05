# Prime number

A number that is divisible by 1 & itself. (2,3,5,7...)

<img width="793" alt="Screenshot 2024-08-05 at 11 03 17 PM" src="https://github.com/user-attachments/assets/488b2615-dd13-4ba8-931c-7350acf490bd">

Consider 36.

<img width="987" alt="Screenshot 2024-08-05 at 11 05 20 PM" src="https://github.com/user-attachments/assets/f9deade5-724f-4a0a-9b3d-9b7371e10205">

If we observe, we can see that the second part is repeating. If we know 3 * 12 gives 36, we don't really need to check if 12 * 3 gives 36 as well.

We can only check for the numbers that are less than square root of the number. This reduces time complexity from n to root n.

### Code:

<img width="444" alt="Screenshot 2024-08-05 at 11 11 15 PM" src="https://github.com/user-attachments/assets/33519411-0fe9-4478-a190-741623436ca3">

### Let's observe another interesting thing.
Let's consider 40. We need to find prime numbers between 0 to 40.

If a number is prime, we know that its multiples will also be prime. We can eliminate those. For example 2 is prime. Its multiples 4,6,8,10 etc
are not prime & hence can be eliminated.

<img width="722" alt="Screenshot 2024-08-05 at 11 18 01 PM" src="https://github.com/user-attachments/assets/6d1757f0-3b48-4c58-95c4-a3eb82e9b72c">

#### How do we eliminate which number is eiminated & which number is taken as a prime number?

We can maintain in a Boolean array where index will refer to a number and its value will be either "true" or "false" dependeing on whether the number is
eliminated or kept for further evaluation.

3 is again prime. Hence, we can eliminate its multiples.

<img width="738" alt="Screenshot 2024-08-05 at 11 21 07 PM" src="https://github.com/user-attachments/assets/05bd746a-8d67-478f-9b36-1b76f600d357">

4 is already eliminated so it can be skipped. Moving forward, all the multiples of 5 will be eliminated.

<img width="778" alt="Screenshot 2024-08-05 at 11 22 40 PM" src="https://github.com/user-attachments/assets/4f9c5156-8e8c-44a0-a12c-34be8f04569e">

6 is already eliminated.

Now, since square of 40 is around 6, we can still further checking for reasons mentioned in the beginning.
So, all the elements that are remaining(marked as true) can be considered as prime numbers between 0 to 40.

<img width="990" alt="Screenshot 2024-08-05 at 11 29 35 PM" src="https://github.com/user-attachments/assets/58d58b53-059f-44cd-bceb-2be338580b95">

### This is known as "Sieve of Eratosthenes"

```
The Sieve of Eratosthenes is an ancient algorithm used to find all prime numbers up to a given limit. It's named after the Greek mathematician
 Eratosthenes, who developed it around 240 BCE. The method works by iteratively marking the multiples of each prime number starting from 2.
The sieve thus produces a list of all prime numbers up to the given limit, making it an efficient way to identify prime numbers. The Sieve of
 Eratosthenes is a simple yet powerful algorithm that has been used for centuries and remains a cornerstone in number theory.
```

### Code:
We can reverse the logic while coding so that we dont have to add an extra loop to make all numbers true initially.

<img width="768" alt="Screenshot 2024-08-05 at 11 36 05 PM" src="https://github.com/user-attachments/assets/cf3bddf6-2fb2-430f-a532-b63f6248e388">
<img width="764" alt="Screenshot 2024-08-05 at 11 36 44 PM" src="https://github.com/user-attachments/assets/48e844c6-89b6-4190-8cd1-c43242233109">

### Complexity Analysis
- Space Complexity: O(n) (auxillary space taken - array)
- Time Complexity: 















