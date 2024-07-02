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

# Cohesion
## How to define Cohesion?

How different software components are related to each other.

```
Cohesion is a fundamental concept in software engineering that refers to the degree to which the elements within a module or a class are logically related to each other. In other words, cohesion measures how well the individual components of a system work together to achieve a specific goal. High cohesion ensures that the module or class has a clear and well-defined purpose, making it easier to understand, maintain, and modify. Low cohesion, on the other hand, can lead to complexity and bugs. Effective cohesion is crucial in software development, as it enhances code readability, scalability, and maintainability.  
```

In our case, saveReminders, validateReminders, printReminders, are not at all related to each other. They are not closely related and hence low in Cohesion. If we think about add and remove, they are somewhat related and are like utility methods for Reminder.

Similar to how we moved print to a separate Class, we can create a utility class for Reminder that can add and remove Reminders.

<img width="730" alt="Screenshot 2024-07-02 at 10 06 29 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/3c881f57-a7ed-4de8-b313-96407527bbe1">

This new Class will only be changed when there'll be a new Reminder operation(add/remove).

<img width="1043" alt="Screenshot 2024-07-02 at 10 09 22 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/45b8cc1f-53da-4211-ae3b-92b709970b73">

# Coupling
## How Software Components are inter-dependent

We should aim to reduce Coupling between different Components. Inter-Dependency between different Components should be less.

```
Coupling in software engineering refers to the degree of interdependence between two or more modules, classes, or systems. It is a measure of how closely they are connected and how changes to one module affect the others. Coupling is important because it affects the maintainability, scalability, and flexibility of software systems. There are several types of coupling, including procedural, functional, and data coupling. In general, a system with low coupling is more modular and easier to maintain than one with high coupling. Effective coupling management is essential for building robust and efficient software systems.
```

In Reminder class, we have done tight Coupling till now. Consider a scenario where we need to change current Reminder Validation logic or add new validations, we would require to update the Reminder Class. 

We can rather move Validation to a new Class. All different sort of Validations can be handled there.

<img width="1009" alt="Screenshot 2024-07-02 at 10 34 14 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/40d8423c-8faa-4466-a79b-03690634a8c4">

Similarly, we can move saveValidation logic to a DAO class to handle all different Database/Filesystem related modifications.

<img width="1047" alt="Screenshot 2024-07-02 at 10 41 42 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/dfd1a4f8-48e0-4984-a48a-0eab6914c4e2">

<img width="770" alt="Screenshot 2024-07-02 at 10 49 40 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a5e7b0b9-da32-428c-b3e7-1e286d0a4de4">

## Note: We need to aim for high Cohesion and loose Coupling

<img width="788" alt="Screenshot 2024-07-02 at 10 50 10 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a100ae9b-2a37-40d2-8320-0273bcd4feeb">
<img width="974" alt="Screenshot 2024-07-02 at 10 50 16 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2f910a98-ac78-4bd6-a094-d147a6e9f48c">

### Final Testing

<img width="1041" alt="Screenshot 2024-07-02 at 10 51 55 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/e981bb3b-61e1-4d18-a069-d24b1650dd7c">
<img width="1224" alt="Screenshot 2024-07-02 at 10 52 56 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/756152c8-02d2-45c5-803b-58d2d0c8d932">
<img width="789" alt="Screenshot 2024-07-02 at 10 52 15 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/1e08fd91-2b59-4d86-b880-10eca230b135">
<img width="595" alt="Screenshot 2024-07-02 at 10 52 43 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/06724033-8d60-4b5f-b251-076ad55f7a53">





