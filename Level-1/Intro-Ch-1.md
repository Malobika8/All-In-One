# Intro

## Monolithic Architecture

```
A monolithic architecture refers to a software design approach where a large, standalone program or system is constructed as a single entity. In this type of architecture, 
all components, layers, and features are tightly coupled and integrated into a single unit. This means that every part of the system is directly visible and accessible to every other 
part. Monolithic architecture is often characterized by a single, large codebase and a flat, linear structure. It is commonly used in traditional software development and can be 
scalable, but it can also be difficult to maintain and extend over time.  
```

A monolithic application is built as a single unified unit while a microservices architecture is a collection of smaller, independently deployable services.

<img width="943" alt="Screenshot 2024-07-10 at 7 22 11 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b5f48376-68d4-42e6-92a4-8909d851ff4c">

Problems/Challenges:
- Scalability: Difficulty in scaling individual components or features without impacting the entire system.
- Any changes in the code lead us to test the entire application.
- Flexibility: Limited ability to make changes or updates without affecting the entire application.
- Maintainability: Complexity and difficulty in debugging and troubleshooting issues.
- Developers may not know all the modules making it harder to get started or fix issues.
  
<img width="848" alt="Screenshot 2024-07-10 at 7 24 43 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/4041a24f-1b09-467e-b7af-bb3c92cc8f92">
<img width="1112" alt="Screenshot 2024-07-10 at 7 23 13 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/fd8cda9f-4d9c-4ec7-972c-7781373df409">
<img width="1142" alt="Screenshot 2024-07-10 at 7 32 28 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/e1f59c4f-4b77-47be-b6fd-2323b7bff05a">
<img width="1127" alt="Screenshot 2024-07-10 at 7 33 50 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/54d18441-1379-46db-b5ac-7c1f0a74a74d">

### We can rather have 4 different small applications/services that can talk to each other.

<img width="1165" alt="Screenshot 2024-07-10 at 7 34 08 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9a8e55dc-2422-4507-8058-5ab88d228dcc">

The UI can talk to microservices. Microservices in itself can interact with each other.

<img width="1074" alt="Screenshot 2024-07-10 at 7 43 33 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/97a684f7-5568-48de-806b-85de8219293c">

#### Pros:
- Independently deployable (Scalable and independently deployable when the load increases)

  <img width="1194" alt="Screenshot 2024-07-10 at 7 50 09 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/bd60118a-843c-476e-bee4-f6d853f4da56">

- Each application can be tested differently
- Code changes on one app/service don't need entire application testing
- Dev working on one service should not require the entire application knowledge

Consider the following example,

<img width="1144" alt="Screenshot 2024-07-10 at 7 40 22 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/346fb969-58e3-42f0-8a62-571b35790c02">
<img width="1084" alt="Screenshot 2024-07-10 at 7 41 12 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8274a88a-0490-4037-b974-547ba5d8f908">
<img width="1038" alt="Screenshot 2024-07-10 at 7 41 31 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/01d5aff5-dc75-4eea-8f9f-070a49aead79">
<img width="1052" alt="Screenshot 2024-07-10 at 7 41 55 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a637197b-31fb-4b51-b00a-83211e277d9a">
<img width="1031" alt="Screenshot 2024-07-10 at 7 42 20 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/4e1ccec1-0b33-4e8c-a45a-b17301361b5d">
<img width="1033" alt="Screenshot 2024-07-10 at 7 42 46 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/f3b2fab8-ce18-45b3-9b2d-66154d692725">
<img width="1074" alt="Screenshot 2024-07-10 at 7 43 33 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/fa0304b1-11e2-4a43-84da-48865fd12d8b">

### Notice the difference

<img width="1051" alt="Screenshot 2024-07-10 at 7 44 03 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7f64f805-22a1-40b3-b14f-a1b411b0453f">
<img width="1093" alt="Screenshot 2024-07-10 at 7 44 19 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/0d95a07e-5e41-4be6-830a-617c8f0b2274">


  
