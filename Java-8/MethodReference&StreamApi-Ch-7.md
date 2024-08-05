```
Why method referencing? -> To reuse a method that is existing in the code base.
```

# Types of Method Referencing

<img width="1104" alt="Screenshot 2024-08-05 at 10 19 15 AM" src="https://github.com/user-attachments/assets/478c97a8-feb8-4137-8405-440ab43f1e9a">

1. ### Reference to Static methods:

   Consider the interface IAddition

   <img width="854" alt="Screenshot 2024-08-05 at 10 05 49 AM" src="https://github.com/user-attachments/assets/8db2329b-64bc-4b5b-bbc3-0ba95ddcf8b9">

   We need to provide an implementation for this.

   <img width="1167" alt="Screenshot 2024-08-05 at 10 07 03 AM" src="https://github.com/user-attachments/assets/ed085ae2-70bd-4599-b870-4aa87eccab7f">

   Suppose we already have a method that provides the sum of two integers. We can simply refer to that.

   <img width="679" alt="Screenshot 2024-08-05 at 10 08 33 AM" src="https://github.com/user-attachments/assets/3e64202a-7759-4c25-b68c-01510392673a">

2. ### Reference to an instance/non-static method (of a particular object):

   What if we remove static from the existing "*doAddition()*" method? - We can use the instance name instead of a class name.

   <img width="659" alt="Screenshot 2024-08-05 at 10 13 43 AM" src="https://github.com/user-attachments/assets/52b05bc9-cb5c-47cb-a21e-92647ba07d8d">

   Why don't we directly call the method itself instead of referencing it? - We can invoke the method as per our need. If we call the method
   directly, it will be invoked right away. We might not want that always.

   <img width="1120" alt="Screenshot 2024-08-05 at 10 14 58 AM" src="https://github.com/user-attachments/assets/67a04c16-919c-46af-9c7d-ac8bba84a202">
   <img width="963" alt="Screenshot 2024-08-05 at 10 17 01 AM" src="https://github.com/user-attachments/assets/91b39eed-3ef8-44cf-8100-02425418dac6">
   <img width="956" alt="Screenshot 2024-08-05 at 10 17 12 AM" src="https://github.com/user-attachments/assets/ac415912-ec34-4f77-a2d3-8a31c8c2e1d2">

 3. ### Reference to an instance method of an arbitrary object of a particular type:  

    We can call the "*doAddition()*" method not through the instance object but through an arbitrary object type.

    <img width="840" alt="Screenshot 2024-08-05 at 10 21 14 AM" src="https://github.com/user-attachments/assets/70511bd4-49eb-49de-a347-22c2c64c434d">
    <img width="724" alt="Screenshot 2024-08-05 at 10 22 57 AM" src="https://github.com/user-attachments/assets/4412f826-345d-43a3-947f-a1f81bc23699">
    <img width="709" alt="Screenshot 2024-08-05 at 10 23 08 AM" src="https://github.com/user-attachments/assets/85f05767-6057-49e5-a57e-6dbfc9ab4e9f">

    We can tweak the functional interface a little bit.

    <img width="685" alt="Screenshot 2024-08-05 at 10 24 05 AM" src="https://github.com/user-attachments/assets/143ee595-6215-47c8-ad85-845815c68e60">
    <img width="1060" alt="Screenshot 2024-08-05 at 10 26 31 AM" src="https://github.com/user-attachments/assets/d2333a85-226b-4d6c-9662-1478804dc088">

    It will be converted to this,

    <img width="415" alt="Screenshot 2024-08-05 at 10 28 46 AM" src="https://github.com/user-attachments/assets/08bef9ff-d67a-4394-b63e-c4763a6ce88c">
    <img width="1014" alt="Screenshot 2024-08-05 at 10 29 55 AM" src="https://github.com/user-attachments/assets/462084c1-2b18-4edd-9a9d-7505eed8a772">

    ### Example:

    <img width="761" alt="Screenshot 2024-08-05 at 10 30 30 AM" src="https://github.com/user-attachments/assets/1bfe64d4-7c4b-4d6e-8dac-45bded3d4b27">
    <img width="1008" alt="Screenshot 2024-08-05 at 10 31 55 AM" src="https://github.com/user-attachments/assets/689709e3-bb32-4b9a-aef8-bd5ae0ce48c0">

    Post changes,

    <img width="983" alt="Screenshot 2024-08-05 at 10 33 25 AM" src="https://github.com/user-attachments/assets/05a4683c-56a9-49d0-b2a8-f8ff6c4b37c7">
    <img width="888" alt="Screenshot 2024-08-05 at 10 34 14 AM" src="https://github.com/user-attachments/assets/99c2be65-a8c9-4ee4-a8a5-f7a2d2943252">
    <img width="957" alt="Screenshot 2024-08-05 at 10 34 29 AM" src="https://github.com/user-attachments/assets/9f9716e2-7698-44c4-80c9-724bb930d05a">

    ### More Examples,

    <img width="1167" alt="Screenshot 2024-08-05 at 10 35 53 AM" src="https://github.com/user-attachments/assets/b6a2130f-d294-47ab-a3d7-9cde100ae646">

    ### Example 1: Concat Strings

    <img width="740" alt="Screenshot 2024-08-05 at 10 37 17 AM" src="https://github.com/user-attachments/assets/a587addc-d383-46db-a95d-b9769a174225">

    We can consider BiFunction

    <img width="1058" alt="Screenshot 2024-08-05 at 10 41 03 AM" src="https://github.com/user-attachments/assets/b6210399-1e46-4690-bece-e512524a1693">
    <img width="713" alt="Screenshot 2024-08-05 at 10 41 41 AM" src="https://github.com/user-attachments/assets/8d3e6e5a-005c-488c-a4b4-3c2b77130b1c">

    ### Example 2: Convert to uppercase (Not a good example though)

    Supplier doesn't take anything but returns a String.
    
    <img width="733" alt="Screenshot 2024-08-05 at 10 46 28 AM" src="https://github.com/user-attachments/assets/9d397b7f-7ee2-471d-8406-9679ed38c025">
    <img width="700" alt="Screenshot 2024-08-05 at 10 47 06 AM" src="https://github.com/user-attachments/assets/99350858-e87c-48d9-ad2b-7551433114b9">
    <img width="711" alt="Screenshot 2024-08-05 at 10 47 46 AM" src="https://github.com/user-attachments/assets/c4a67dcf-0298-48e5-afe3-80117286560d">

    We can use Function instead,

    <img width="644" alt="Screenshot 2024-08-05 at 10 51 15 AM" src="https://github.com/user-attachments/assets/3f770bba-1db1-4e3d-a7b9-0396783d0d61">
    <img width="750" alt="Screenshot 2024-08-05 at 10 52 31 AM" src="https://github.com/user-attachments/assets/2f4f93e4-f26b-4fd7-833c-18eb00d9e458">

    












   

   
