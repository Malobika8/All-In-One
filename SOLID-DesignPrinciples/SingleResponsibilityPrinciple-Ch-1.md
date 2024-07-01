### Solid design principles are a set of guidelines for building clean, maintainable, and scalable software architecture. SOLID stands for five design principles:

1. Single Responsibility Principle (SRP): Each component should have only one reason to change.
2. Open-Closed Principle (OCP): A class should be open for extension but closed for modification.
3. Liskov Substitution Principle (LSP): Subtypes should be substitutable for their base types.
4. Interface Segregation Principle (ISP): Clients should not be forced to depend on interfaces they don't use.
5. Dependency Inversion Principle (DIP): High-level modules should not depend on low-level modules, but both should depend on abstractions.

## Agenda
- Create a Reminder App
- The app should keep all the reminders in a file and store it somewhere
- Follow as per the design principles

Let's try to look at the UML(Unified Modeling Language) diagram.

```
UML stands for Unified Modeling Language, a graphical representation language used to design, visualize, and document the architecture of software systems, as well as other complex
systems.
```
<img width="598" alt="Screenshot 2024-07-01 at 10 26 09 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/af576337-dcbc-4bdd-b0fe-9534202b9761">

### Reminder

<img width="980" alt="Screenshot 2024-07-01 at 10 38 10 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/35f833e5-c628-4ac8-8515-bb174497391a">
<img width="1047" alt="Screenshot 2024-07-01 at 10 38 22 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/f588229d-a42e-4a81-9c93-37c2367122eb">
<img width="985" alt="Screenshot 2024-07-01 at 10 38 31 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/1421697a-1afa-4049-b57e-3901c46c5183">

### Main

<img width="1047" alt="Screenshot 2024-07-01 at 10 38 41 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/539def5b-1ebe-449f-937e-3ed4e85775c8">

## The code that we have written works but doesn't meet Industry Standard. 

It doesn't follow any Design Principle. Moreover, the class works for everything and covers every functionality which should'nt be the case.

# Single Responsibility Principle

<img width="1102" alt="Screenshot 2024-07-01 at 1 06 29 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c5ac441c-9376-46ad-8d39-df3a114feef3">
<img width="1119" alt="Screenshot 2024-07-01 at 1 07 05 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/376b2be2-7e4f-46bc-a653-5f5c79b1b6dc">

This says that a Class should have only one *Responsibility*. It should do a specific task rather than handling all.

<img width="1073" alt="Screenshot 2024-07-01 at 10 49 45 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/64a7f1ea-9025-4005-9625-418c55247d15">

Our **Reminder Class** violates the Single Responsibility Principle as it does a lot of things (save, validate, remove etc).

## How to define Responsibilty?

<img width="987" alt="Screenshot 2024-07-01 at 10 58 51 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a8c240af-e668-4c43-b945-f9f8043acc78">
<img width="824" alt="Screenshot 2024-07-01 at 11 03 20 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/f8e35034-40db-45a2-8745-6107a974d87a">

In current scenario, if we want to change something ( update validate logic or maybe print in some other format), we would need to update Validate Class again and again. This should be
avoided. 

<img width="438" alt="Screenshot 2024-07-01 at 11 05 00 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b9c0eaf5-db19-4700-9cd0-903311c82104">

SRP says that we should rather separate Classes based on functionalities. For eg. a print class to handle all print related tasks.

<img width="759" alt="Screenshot 2024-07-01 at 11 08 04 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/34314444-7773-4618-87d8-26385963ff3f">

## How to define Cohesion?






