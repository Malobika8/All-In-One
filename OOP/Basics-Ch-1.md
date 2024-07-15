## Brush Up
- Garbage collection happens automatically to free memory. We don't have to do it ourselves but we can tell what to do by overriding the "finalize()" method. We don't need to call this   method as it is called automatically during garbage collection.

  <img width="784" alt="Screenshot 2024-07-15 at 8 56 15 PM" src="https://github.com/user-attachments/assets/d6dac31c-137d-46d8-9d0a-564404d1ffd8">
  <img width="1144" alt="Screenshot 2024-07-15 at 8 58 36 PM" src="https://github.com/user-attachments/assets/ce0cab42-85b8-4e06-a156-0754e5e94174">

- Consider a class and object of that class. When we print the object, it checks if there's a "toString()" method available in our class. If yes, it prints whatever is there in that      method. Otherwise, it calls the default "toString()" method which basically prints the Hashcode.

  <img width="776" alt="Screenshot 2024-07-15 at 9 09 26 PM" src="https://github.com/user-attachments/assets/769518d1-2a10-4ab0-bbde-53f66c4ba49b">
  <img width="775" alt="Screenshot 2024-07-15 at 9 09 37 PM" src="https://github.com/user-attachments/assets/1b2b126d-d967-41cf-a31f-624b5c541953">
  <img width="769" alt="Screenshot 2024-07-15 at 9 10 05 PM" src="https://github.com/user-attachments/assets/4d099bf7-fed0-4196-9a44-921ba6e7cb7b">

  Default "toString()" method,

  <img width="776" alt="Screenshot 2024-07-15 at 9 10 20 PM" src="https://github.com/user-attachments/assets/75b5ed87-4ad0-4b1c-ae9a-e8a24191a7fb">

- From static, we cannot use non-static stuff. To use non-static items, we need to use object Reference.
- We have some static variables. We want to initialize our static variables. We can do that via a static block. that block gets executed exactly once when that class is loaded.

  <img width="935" alt="Screenshot 2024-07-15 at 10 09 22 PM" src="https://github.com/user-attachments/assets/1573c898-b30a-4436-926b-643338d1b118">
  <img width="766" alt="Screenshot 2024-07-15 at 10 08 22 PM" src="https://github.com/user-attachments/assets/843bd2d2-7d29-403b-89cf-a1a50e43b565">

- Only Inner classes can be static
## Packages

