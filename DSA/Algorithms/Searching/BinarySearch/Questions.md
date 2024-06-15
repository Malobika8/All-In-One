## How do we know when to apply binary search? 
If in the prolem statement, we are given a sorted array, we can try binary search first. Other problem statements include something like we
are required to get one particular answer & we are following a continuous sequence to get that answer.

Eg. sq root of a number

## Q1. Ceiling of a given number (Find the smallest number that is greater than or equal to target)

https://leetcode.com/problems/search-insert-position/

<img width="1142" alt="Screenshot 2024-06-15 at 11 31 57 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/0b3350a5-0d99-4335-a9ec-02fc921e6702">
<img width="1019" alt="Screenshot 2024-06-15 at 12 38 37 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/af90094b-2b99-42e5-8e18-b6e735fbef94">
<img width="1022" alt="Screenshot 2024-06-15 at 12 38 51 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/6b90412f-0bff-4544-82fc-e6efbd115996">

<img width="811" alt="Screenshot 2024-06-15 at 12 39 43 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/11b00982-f1a2-43da-a8d1-5a11c1debf2c">

## Q2. Find the floor of a number (Find the largest number that is lesser than or equal to target)

<img width="1013" alt="Screenshot 2024-06-15 at 12 45 58 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ad3293c2-09c7-4cd9-b2ef-12f654270fe9">
<img width="1012" alt="Screenshot 2024-06-15 at 12 46 06 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/67aa98f1-a714-42d3-8d4c-01d883b0ec4b">

Same as above. Consider "end" this time.

## Q3. Find smallest letter greater than the target

https://leetcode.com/problems/find-smallest-letter-greater-than-target/description/

<img width="1007" alt="Screenshot 2024-06-16 at 12 25 05 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/03fcb3a4-caeb-4894-a573-9cab153f3bcb">
<img width="1002" alt="Screenshot 2024-06-16 at 12 25 17 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2bcda1ed-6c57-47ff-8380-74023b3e6e71">

<img width="802" alt="Screenshot 2024-06-16 at 12 38 44 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/24f5f8c4-974c-4571-9160-72394c3190b2">

Or we can also just return "letters[start % letters.length]".

## Q4. Find First and Last Position of Element in Sorted Array

https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/description/

We can solve this using linear search as well in O(n) time. However, better would be to do using binary search as time would then reduce to 
O(log n).

Run binary search twice - to find first occurrence of target and last occurrence of target

<img width="1018" alt="Screenshot 2024-06-16 at 1 30 04 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/f45e6de3-a2f2-4d61-8dbd-c46c16002333">

<img width="763" alt="Screenshot 2024-06-16 at 1 25 54 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7d41d60b-0685-427f-9e2a-e3d6ec891028">
<img width="814" alt="Screenshot 2024-06-16 at 1 26 27 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ea7b2e17-c74b-42e6-b6b1-7bab5dfd84cf">

## Q5. Position of an Element in Infinite Sorted Array

https://www.geeksforgeeks.org/find-position-element-sorted-array-infinite-numbers/

<img width="669" alt="Screenshot 2024-06-16 at 1 33 01 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/cb8909e0-182f-4af8-b851-959b35de2404">


