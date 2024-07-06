## Need of Variable length arguments

Consider a scenario where we want to add two numbers.

We can have a method that takes two arguments and returns the sum. Similarly to add 3 or more numbers, we can do method overloading.

<img width="1000" alt="Screenshot 2024-07-05 at 3 51 14 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/fbe8592e-10b3-48ca-ac83-8bee7ae22717">

However, this approach isn't good as it leads to Code Redundancy.

#### How to solve this then?

In Java 1.5, variable length argument was introduced. Whenever we are not sure about the number of arguments in a method, we can make use of
variable arguments (aka varargs).

<img width="1169" alt="Screenshot 2024-07-05 at 3 56 40 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/08e19553-0805-4064-8f72-0e6d633b80a6">

Previously, we were creating different methods with multiple arguments based on how many numbers we wanted to find the sum of.

Instead of that, we can now use varargs and find sum of as many numbers as we want.

<img width="718" alt="Screenshot 2024-07-06 at 10 48 20 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9715d0c8-d7b5-45d7-9627-8205db3c233e">

## Note:
The 3 ellipses denote nothing but an array

#### *int[] numbers* is same as *int...numbers*

<img width="1133" alt="Screenshot 2024-07-06 at 10 52 55 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/eb127c25-b37a-425a-8996-eb1135546f99">
<img width="1010" alt="Screenshot 2024-07-06 at 10 53 34 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/cf80c7f1-1b71-44e3-b26b-a3bc72775454">

Unlike the first approach, varargs accept a bunch of numbers as well along with an array of numbers.

<img width="590" alt="Screenshot 2024-07-06 at 10 56 06 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/92e1389f-db48-4ce4-93ca-ea53105e9ba8">

### Difference between taking an array as a parameter and taking a varargs

<img width="1149" alt="Screenshot 2024-07-06 at 10 56 43 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/06c0f0ff-e404-439f-91f3-7d8e5c86c8d9">
<img width="1144" alt="Screenshot 2024-07-06 at 10 57 07 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a3ebf676-d87f-42ee-aa78-9506ff60f82b">

Let's now make this function work.

<img width="1089" alt="Screenshot 2024-07-06 at 10 59 16 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/528a40e1-a108-49d4-a734-f735627b99c7">

## FYI

We can even use varargs in main method as it uses *String[]* (String array)

<img width="563" alt="Screenshot 2024-07-06 at 11 03 17 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/fe87f8df-7cef-4eae-a8d6-52a867901fc0">

## Question

<img width="1000" alt="Screenshot 2024-07-06 at 11 11 33 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d4a0cdd1-3089-4eff-901d-c5e63ddd3274">

Ans: None of the above
