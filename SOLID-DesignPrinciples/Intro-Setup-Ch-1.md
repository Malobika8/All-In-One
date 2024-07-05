# SOLID Design Principles

SOLID is an acronym for first five Object Oriented Design principles by *Robert C. Martin.*

It's a set of guidelines for building clean, maintainable, and scalable software architecture. SOLID stands for five design principles:

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
