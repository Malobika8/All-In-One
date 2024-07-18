# map()

Print only the numbers which are greater than 5.

<img width="1081" alt="Screenshot 2024-07-18 at 3 16 41 PM" src="https://github.com/user-attachments/assets/6ad35184-5e29-4788-894e-bf1e632c03ca">

### Requirement: Numbers should be transformed to words while printing to console

We have a straightforward method called *map()* that can help us do this.

<img width="1147" alt="Screenshot 2024-07-18 at 3 18 49 PM" src="https://github.com/user-attachments/assets/267fefb4-cac8-4147-878b-a9538908f798">

*map()* takes a "Function" (It takes an input and returns an output).

<img width="776" alt="Screenshot 2024-07-18 at 3 30 22 PM" src="https://github.com/user-attachments/assets/fecd5ef1-0a25-4411-89e6-eedba0824275">
<img width="790" alt="Screenshot 2024-07-18 at 3 26 57 PM" src="https://github.com/user-attachments/assets/061ff774-6c43-4c01-b999-884757a21685">
<img width="834" alt="Screenshot 2024-07-18 at 3 27 23 PM" src="https://github.com/user-attachments/assets/f966caef-a2e7-49a7-a2e0-f875283fa10d">

#### Note: The operations like filter(), map() are Internediate Operations.

<img width="856" alt="Screenshot 2024-07-18 at 3 31 52 PM" src="https://github.com/user-attachments/assets/6b1cd1d9-890a-4eb3-9739-23e53113ac91">

### Note:
- Whenever a method returns a stream of something, it is always considered as an "Intermediate Operation".
- When a method doesn't return a stream of something, it is considered as "Terminal Operation". Ex: *forEach()*

Let's add a log in the existing code and observe,

<img width="1049" alt="Screenshot 2024-07-18 at 3 36 02 PM" src="https://github.com/user-attachments/assets/1beb997f-c3cc-41e8-aa9c-d451c33f2191">
<img width="1056" alt="Screenshot 2024-07-18 at 3 36 22 PM" src="https://github.com/user-attachments/assets/d5c2f688-99f2-4f63-b56a-fe81b0ec0c01">

#### Output

<img width="766" alt="Screenshot 2024-07-18 at 3 37 27 PM" src="https://github.com/user-attachments/assets/1d7c1a0d-e5a1-4fe4-98b3-6dad1256df8f">

### What will happen if we comment out *forEach()* method?

- It won't print anything. None of our Intermediate operations (filter(), map()) will be executed.
- Stream is lazy in nature
- It will only be invoked if any Terminal operation takes place.
- Terminal operation triggers/starts a stream.

## collect()
### What if we want to collect stream to List?

We can use the *collect()* method. *collect()* is again a Terminal Operation.

<img width="870" alt="Screenshot 2024-07-18 at 3 42 01 PM" src="https://github.com/user-attachments/assets/9791e1cd-0b88-4ae8-a7ce-0def1ad052fb">

## count()
### Count the number of elements present in mappedStream

<img width="1052" alt="Screenshot 2024-07-18 at 3 43 45 PM" src="https://github.com/user-attachments/assets/f9bc9900-7710-43fc-9d56-4eed537b4040">

*count()* is again a Terminal operation.

#### Note: Terminal operations trigger a stream as well as terminate it.

<img width="1147" alt="Screenshot 2024-07-18 at 3 46 27 PM" src="https://github.com/user-attachments/assets/4a4955b9-bdd0-4b04-a8d8-99ceb2cb759d">

## Assignment

Consider *Student* class and *getStudentList()* method

<img width="791" alt="Screenshot 2024-07-18 at 3 47 36 PM" src="https://github.com/user-attachments/assets/16786d05-648d-4984-99af-bafa83a1b963">

Q. Print the first 2 Student's names from the Student List whose age is greater than 25.

We can use *limit()* method,

<img width="919" alt="Screenshot 2024-07-18 at 3 55 23 PM" src="https://github.com/user-attachments/assets/dde1a1b4-3eb3-4a79-9809-3557f1e2cf12">
<img width="801" alt="Screenshot 2024-07-18 at 3 55 49 PM" src="https://github.com/user-attachments/assets/0d01df98-0a5b-4b6d-bc1b-0becd03e9233">

We can even collect it in a List and then print it.

<img width="1049" alt="Screenshot 2024-07-18 at 3 56 29 PM" src="https://github.com/user-attachments/assets/70e0550c-f402-403b-9a39-003fd18654f5">
