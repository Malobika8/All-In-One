# Recursion
### Function calling itself

Suppose we want to print numbers upto 5. We can have 5 print methods. All the methods can call the one that is next in line.

<img width="722" alt="Screenshot 2024-07-03 at 1 19 20 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/fd4668e3-bd49-4676-a462-7f33a3138c6f">

If we notice, the body and method parameter is same for all. Just the method name is different.

### Note:
All the function calls that happens in a Programming Language goes to Stack memory.

#### How function call works?
- While the function is not finished executing, it remains in the Stack
- When a function finishes executing, it is removed from the Stack & the flow of Program is restored to where the function was called.

<img width="227" alt="Screenshot 2024-07-03 at 1 29 32 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/f3096401-6867-44d2-b16b-fa2a267a992f">
<img width="1023" alt="Screenshot 2024-07-03 at 1 32 59 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/54bfe4e7-5d1b-4109-bb4a-e7b455c1425b">

In the above example, if we observe, we can see that there's repetition happening. So, instead of creating another function, we can just let 
the function call itself.

Everytime we can increment the number and call the same function.

There's a special case though which is basically the last *print5()* method. If we notice, it doesn't call any other function. We can take this 
as a stopping condition also known as *Base Case*. In absence of Base comdition, Stack will keep getting called again and again. We know every 
call takes some memory. So, there will come a point when all of the memory will be exhausted. This is called StackOverflow.

<img width="685" alt="Screenshot 2024-07-03 at 1 41 35 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d0c1d033-bd7c-43ee-95d8-249bf17be892">

#### Base Condition: It is a condition where our Recursion stops making new calls.

<img width="1011" alt="Screenshot 2024-07-03 at 2 53 23 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7062f16c-b88e-4010-9a42-b6219a243c5a">

### Why Recursion?

- It helps in solving bigger/complex problems in a simple way.
- We can convert Recursion solution into Iteration and vice-versa.
- Space complexity is not constant because of Recursive calls.
- It helps us in breaking down bigger problems into smaller problems.

### How to study Recursion?

### Recursion Tree
In order to solve any Recursion problem, we should be able to visualise Recursion calls.

<img width="1016" alt="Screenshot 2024-07-03 at 2 58 49 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/10abe1ac-6cdb-47d4-adbf-30d3cb59f10e">




