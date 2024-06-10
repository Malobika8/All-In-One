# Stack

### What is Stack?

<img width="946" alt="Screenshot 2024-06-10 at 7 29 15 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/e930622d-d495-40cf-b4bc-303f503e8772">
<img width="954" alt="Screenshot 2024-06-10 at 7 32 05 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/9f19a634-fa74-4ced-9675-a2e6e4118d01">
<img width="936" alt="Screenshot 2024-06-10 at 7 34 45 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/ee940467-e681-4d61-968e-dcd26e2f0e9d">

- Push Operation:

  <img width="981" alt="Screenshot 2024-06-10 at 7 38 52 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/7b921090-0fe9-4b34-9ebc-4d338dda1305">

- Pop Operation:

  <img width="883" alt="Screenshot 2024-06-10 at 7 41 49 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/9c4ca7a5-f1ff-487a-8f81-17afa0da9938">

## Analysis

<img width="877" alt="Screenshot 2024-06-10 at 7 42 13 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/cc4c529a-f79c-4be6-b24d-b6ca58b0fe3b">

## Application of Stack

<img width="940" alt="Screenshot 2024-06-10 at 7 46 03 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/366b22bf-08aa-4b08-a08a-a30ca1a43284">

## Tower Of Hanoi

*What is the Tower of Hanoi?*

The Tower of Hanoi is a mathematical puzzle. It consists of three rods and N disks. The task is to move all disks to another rod following certain rules:

- Only one disk can be moved at a time.
- Only the uppermost disk can be moved from one stack to the top of another stack or to an empty rod.
- Larger disks cannot be placed on top of smaller disks.

*Total no of Transactions:* **2^n -1** (n = Total no of Disks)

<img width="958" alt="Screenshot 2024-06-10 at 7 51 13 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/4c61c5fc-81ef-4c79-a203-2481a952f6ea">
<img width="298" alt="Screenshot 2024-06-10 at 7 51 59 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b61d5e6a-b75e-4995-a531-3f2ec604b589">

*Recursive method for Tower Of Hanoi*

<img width="788" alt="Screenshot 2024-06-10 at 7 59 57 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/197dd65b-55d2-4d11-8c48-894e1722d866">

## Evaluation of Postfix and Prefix Expression

- Postfix: **((B X A) where B = next to Top element & A = Top element)**

  <img width="953" alt="Screenshot 2024-06-10 at 8 26 00 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/c67b1751-4f15-4cff-ba94-1b1e363731be">
  <img width="632" alt="Screenshot 2024-06-10 at 8 26 57 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/87caaa8a-c61d-4637-870d-bae72ddc8ae4">

- Prefix: **((B X A) where B = Top element) & A = next to Top element**

  Evaluate the expression and then reverse it.

  <img width="797" alt="Screenshot 2024-06-10 at 8 27 30 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/cebc7016-91b8-45f8-a83f-312b85a65b65">
  <img width="333" alt="Screenshot 2024-06-10 at 8 28 25 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/cb100883-6776-48af-ab12-c47814444b0c">
  <img width="702" alt="Screenshot 2024-06-10 at 8 31 31 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/44e249f0-6d56-4c05-8103-13ce81f10041">

## Converting Infix Expression into Postfix Expression

*Preference:*

<img width="321" alt="Screenshot 2024-06-10 at 8 33 29 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/1905f504-f485-499d-b405-38321279a5fc">

- To Postfix Expression:

  * Example 1:
  
    <img width="789" alt="Screenshot 2024-06-10 at 8 32 41 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/2e593310-8d0c-4479-9864-7199be30a231">
    <img width="820" alt="Screenshot 2024-06-10 at 8 34 54 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/0b6809f1-d528-431f-bffb-5e3c338d380e">

  * Example 2:

    <img width="871" alt="Screenshot 2024-06-10 at 8 41 41 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/dc34657c-1128-49eb-bd66-5dd9de0cc6be">

  * Using Stack:
    - A higher priority operator can stay above lower priority operator
    - A lower priority operator cannot stay above higher priority operator. If we encounter a lower operator, transfer the higher operator to expression P
    - Same priority operators cannot stay together. If we encounter a same priority operator, transfer the existing operator to expression P
    - If we encounter a closing bracket, cancel out the opening bracket
   
      <img width="826" alt="Screenshot 2024-06-10 at 8 51 52 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/e87bbf0f-c039-49ad-8cb6-e5ef21c44cb0">
      <img width="838" alt="Screenshot 2024-06-10 at 8 54 17 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/ccc8bff6-e81f-42c2-be17-e8cc8da4f8a6">

- To Prefix Expression:

  * Example 1:

    <img width="846" alt="Screenshot 2024-06-10 at 8 37 44 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/fd83b424-056f-445d-99ed-2fca84d7ac03">

  
