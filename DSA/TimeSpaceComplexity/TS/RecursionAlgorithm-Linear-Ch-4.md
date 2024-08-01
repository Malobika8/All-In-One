# Solve homogeneous linear Recurrence Relation (don't have any separate function like g(x))

We can find formulas for these relations which can give us answers in a single step.

Let's take the example of Fibonacci Number.

Form of linear Recurrence Relation,

<img width="1012" alt="Screenshot 2024-07-31 at 3 03 26 PM" src="https://github.com/user-attachments/assets/1481688f-26df-4291-b5a0-2e723c48379c">

Recurrence Relation for Fibonacci,

<img width="1015" alt="Screenshot 2024-07-31 at 8 58 39 PM" src="https://github.com/user-attachments/assets/224c699e-db88-459d-adbd-41499675b4cc">

### Steps:
- Step 1:

  <img width="1012" alt="Screenshot 2024-07-31 at 8 58 33 PM" src="https://github.com/user-attachments/assets/8ec8ca99-0e02-4a53-9529-ec79b8341640">
  <img width="1016" alt="Screenshot 2024-07-31 at 9 00 27 PM" src="https://github.com/user-attachments/assets/1a33a7da-33f2-42b4-b0d5-008e5f3417cd">
  <img width="1005" alt="Screenshot 2024-07-31 at 9 00 37 PM" src="https://github.com/user-attachments/assets/b1120801-08c8-4bca-b48d-614f3d614f54">

- Step 2: If we have α1 & α2 as two roots, we can write it as,

  <img width="913" alt="Screenshot 2024-07-31 at 8 59 48 PM" src="https://github.com/user-attachments/assets/ccc7afbb-eade-475f-ac3a-5526c2ff9f22">
  <img width="1010" alt="Screenshot 2024-07-31 at 9 01 13 PM" src="https://github.com/user-attachments/assets/383a1c87-8f7a-4eda-b413-dd58dc96a4d2">
  <img width="1011" alt="Screenshot 2024-07-31 at 9 01 24 PM" src="https://github.com/user-attachments/assets/3eb8941d-fa80-40a7-b94b-c3b59152a99f">

- Fact: No of roots that we have is equal to the number of answers that we have.

  <img width="999" alt="Screenshot 2024-07-31 at 11 18 20 PM" src="https://github.com/user-attachments/assets/5f5200ab-b25c-43c9-a292-f87c24195261">
  <img width="1012" alt="Screenshot 2024-07-31 at 11 18 28 PM" src="https://github.com/user-attachments/assets/0d062b03-1086-4c39-92df-d5165449e607">
  <img width="1008" alt="Screenshot 2024-07-31 at 11 18 36 PM" src="https://github.com/user-attachments/assets/10c4c96a-9f9d-45be-a4b1-ccbbb58857f5">
  
  ### We got the formula for the nth Fibonacci number. We can use this directly. No need to run recursion or even iteration. 😁

  This would have taken a lot of time if we had done recursively. It wouldn't even work for 50.
  
  <img width="1136" alt="Screenshot 2024-07-31 at 11 28 39 PM" src="https://github.com/user-attachments/assets/5d5b007e-5574-4b8f-a53a-facb2ef48a69">
  <img width="382" alt="Screenshot 2024-07-31 at 11 28 47 PM" src="https://github.com/user-attachments/assets/63e69616-5203-40fc-b5e6-0a51724d817f">

  ### How to find the time complexity from this?

  <img width="1018" alt="Screenshot 2024-07-31 at 11 25 01 PM" src="https://github.com/user-attachments/assets/b70b13cc-e139-40bf-a555-ebb954c53176">

  Golden ratio of Mathematics.

  <img width="1015" alt="Screenshot 2024-07-31 at 11 25 10 PM" src="https://github.com/user-attachments/assets/f59f9582-871b-4ba4-9a25-a6e1ad751368">

  ## We might get equal roots

  <img width="1013" alt="Screenshot 2024-07-31 at 11 38 38 PM" src="https://github.com/user-attachments/assets/acb4ec02-1728-4a86-a8e9-29307c0d2d18">
  <img width="1018" alt="Screenshot 2024-07-31 at 11 38 45 PM" src="https://github.com/user-attachments/assets/df28073f-732d-4290-bf93-7cf6ca08589e">
  <img width="1020" alt="Screenshot 2024-07-31 at 11 38 54 PM" src="https://github.com/user-attachments/assets/5a882ee8-3fec-441e-bb01-af439f6f8089">
  <img width="1015" alt="Screenshot 2024-07-31 at 11 39 01 PM" src="https://github.com/user-attachments/assets/c0069dd2-24d0-4277-80a0-28ee16168bef">

# Non-homogeneous linear recurrence (there's extra function g(n))

Form

<img width="1016" alt="Screenshot 2024-07-31 at 11 42 22 PM" src="https://github.com/user-attachments/assets/9a785d5f-76e3-448c-bb57-98ed5ef2cb0f">

## How to solve

Steps:

- Replace g(n) with 0 & solve usually.

  <img width="1010" alt="Screenshot 2024-07-31 at 11 50 29 PM" src="https://github.com/user-attachments/assets/84ae9f64-9088-4c03-8082-4fb5918fccea">
  <img width="1008" alt="Screenshot 2024-07-31 at 11 50 39 PM" src="https://github.com/user-attachments/assets/59fb1504-b461-4bbb-b504-92f3bf11fd54">

- Put g(n) on one side and find a particular n.

  <img width="1022" alt="Screenshot 2024-08-01 at 12 50 15 PM" src="https://github.com/user-attachments/assets/50e2b451-fc58-421a-9c06-ca1c39d2e0f4">

- Add both solutions together.

  <img width="1006" alt="Screenshot 2024-08-01 at 12 50 25 PM" src="https://github.com/user-attachments/assets/072a5868-2b72-4d25-85f5-e559713f8023">

## How do we guess a particular solution?

- If g(n) is exponential, guess of the same type.

  <img width="997" alt="Screenshot 2024-08-01 at 12 51 34 PM" src="https://github.com/user-attachments/assets/8db4567a-cde8-41e3-9d22-59128366362e">
  
- If it is polynomial, guess of the same degree.

  <img width="1014" alt="Screenshot 2024-08-01 at 12 52 45 PM" src="https://github.com/user-attachments/assets/06e36204-354b-44b3-aef4-54defb72288e">

- If it fails, try for the next degree.

  <img width="1014" alt="Screenshot 2024-08-01 at 12 53 53 PM" src="https://github.com/user-attachments/assets/80784d47-6583-4834-b1a9-fa0f7cdedf0b">

  Example:

  <img width="1003" alt="Screenshot 2024-08-01 at 12 54 01 PM" src="https://github.com/user-attachments/assets/15a29c06-93ea-450f-8404-c897f079c4af">
  <img width="1010" alt="Screenshot 2024-08-01 at 12 54 10 PM" src="https://github.com/user-attachments/assets/e7bf387b-2584-4ff0-aaa9-3423ffc5730f">
  <img width="1017" alt="Screenshot 2024-08-01 at 12 54 17 PM" src="https://github.com/user-attachments/assets/fc17cff6-a7fe-46cb-a40d-c7e058f56701">

  General answer:

  <img width="1009" alt="Screenshot 2024-08-01 at 12 55 08 PM" src="https://github.com/user-attachments/assets/810431a6-823d-4da8-a448-b2741b2b8840">



  


  





  

  




  


