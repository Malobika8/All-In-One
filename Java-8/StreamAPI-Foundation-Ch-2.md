# filter()
Suppose we have an array of integers. 

<img width="831" alt="Screenshot 2024-07-18 at 2 35 27 PM" src="https://github.com/user-attachments/assets/198d0b21-9249-4510-991c-8646c7601853">

Old way to do this / Imperative approach,

<img width="1003" alt="Screenshot 2024-07-18 at 2 36 39 PM" src="https://github.com/user-attachments/assets/cf968176-b77d-4165-8dbc-1827d367ace0">

We can do the same using StreamAPI. We can use this array as source.

<img width="870" alt="Screenshot 2024-07-18 at 2 40 25 PM" src="https://github.com/user-attachments/assets/da45ee93-d027-480d-862e-61090d7c22c2">
<img width="861" alt="Screenshot 2024-07-18 at 2 45 44 PM" src="https://github.com/user-attachments/assets/c38a61c0-bf7d-4bf2-bf08-d3da41e65ad7">

Before printing, we can add a filter logic. If the condition is satisfied, then we can print the numbers.

There's a method called *filter()* that takes a Predicate(Predicate is again a Functional Interface).

Predicate is something which is used in Java in order to evaluate if something is true or false.

<img width="839" alt="Screenshot 2024-07-18 at 2 49 10 PM" src="https://github.com/user-attachments/assets/b450758e-2156-400f-a5d4-649cf5418a90">
<img width="746" alt="Screenshot 2024-07-18 at 2 49 52 PM" src="https://github.com/user-attachments/assets/a3edf262-4b63-4a68-88a6-e61e773bea97">

*filter()* method creates a new stream of integers that satisfies a condition.

<img width="719" alt="Screenshot 2024-07-18 at 2 51 24 PM" src="https://github.com/user-attachments/assets/b8bc4bca-98cb-4f3a-8e96-5bc275bc7e21">
<img width="1138" alt="Screenshot 2024-07-18 at 2 52 42 PM" src="https://github.com/user-attachments/assets/323010a8-7edb-4618-9514-16d7b0d089c8">

*Note: here, stream does actual iteration*

<img width="1149" alt="Screenshot 2024-07-18 at 2 56 10 PM" src="https://github.com/user-attachments/assets/d7e2ef8e-a2ad-4b04-b44d-5f0c230bc06c">

#### Note: *filter()* is an intermediate operation between source and destination.

We can simplify it as done earlier.

<img width="1078" alt="Screenshot 2024-07-18 at 2 58 08 PM" src="https://github.com/user-attachments/assets/42bd5be0-4a7d-4db6-827a-27e4da940f2a">
<img width="974" alt="Screenshot 2024-07-18 at 2 58 50 PM" src="https://github.com/user-attachments/assets/c213a590-d059-4e3b-8253-ddb86648bfef">
<img width="869" alt="Screenshot 2024-07-18 at 3 03 50 PM" src="https://github.com/user-attachments/assets/0e6cc43a-b013-4b8d-a3ff-ea8ec17822ef">

<img width="1148" alt="Screenshot 2024-07-18 at 2 59 38 PM" src="https://github.com/user-attachments/assets/073cf079-dcb0-4ae0-a998-b88807da5b23">
<img width="1147" alt="Screenshot 2024-07-18 at 3 00 20 PM" src="https://github.com/user-attachments/assets/f78408e8-851c-4994-8c39-35a07a33c81e">
<img width="1145" alt="Screenshot 2024-07-18 at 3 02 07 PM" src="https://github.com/user-attachments/assets/35aae58a-66f7-43a6-b9e0-414f57838bc8">

### Note: Numbers are passed through the stream one by one

<img width="1148" alt="Screenshot 2024-07-18 at 3 02 41 PM" src="https://github.com/user-attachments/assets/65332c0c-3e90-4eff-82f8-b95c35cc7b98">
<img width="874" alt="Screenshot 2024-07-18 at 3 07 48 PM" src="https://github.com/user-attachments/assets/b9a272d8-9cf3-47d7-8182-4cf5231db40e">
<img width="799" alt="Screenshot 2024-07-18 at 3 08 10 PM" src="https://github.com/user-attachments/assets/b3aad2c3-4235-4e0d-97ac-c75a6bb00a90">
<img width="805" alt="Screenshot 2024-07-18 at 3 09 24 PM" src="https://github.com/user-attachments/assets/80465835-6b88-4ac4-9239-bc163fb1b9ef">

streams are immutable in nature

<img width="1004" alt="Screenshot 2024-07-18 at 3 10 06 PM" src="https://github.com/user-attachments/assets/906293ac-8b38-4268-9a7a-3a47c35a158b">
<img width="1009" alt="Screenshot 2024-07-18 at 3 10 38 PM" src="https://github.com/user-attachments/assets/e6cde060-d8f3-4a72-a1c3-e71df9f11a37">
<img width="1014" alt="Screenshot 2024-07-18 at 3 12 28 PM" src="https://github.com/user-attachments/assets/640144a8-bf07-4082-9ab0-4ec7c7025fe4">

















## Check your knowledge

Q. What is the use of Consumer in Java
