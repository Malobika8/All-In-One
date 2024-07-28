
Suppose that we have a Functional Interface. Functional Interface has only one abstract method.

<img width="1061" alt="Screenshot 2024-07-28 at 10 55 12 PM" src="https://github.com/user-attachments/assets/1f7c4f70-7ed5-4ade-87a7-7014795ca349">

### How can we provide implementation to it?

- 1st option would be to simply have an implementation class that implements the Functional Interface.
- The 2nd option would be to have an anonymous inner-class

  <img width="659" alt="Screenshot 2024-07-28 at 10 36 36 PM" src="https://github.com/user-attachments/assets/69dadcce-97ad-440a-aded-91e06350e4d3">

  We have to write a lot of code for this

# Lambda Expression
A good replacement is to use Lambda. We can convert the anonymous class to lambda.

<img width="1014" alt="Screenshot 2024-07-28 at 10 40 15 PM" src="https://github.com/user-attachments/assets/8ad4e999-b32d-49d7-89fb-c0de4d69baa2">

We can reduce it even further.

<img width="991" alt="Screenshot 2024-07-28 at 10 41 12 PM" src="https://github.com/user-attachments/assets/9a36271e-cd84-4fb9-b383-db3efda63f09">

Suppose we have a method that already exists that returns the sum of two numbers. For the abstract method present in our Functional Interface,
suppose we don't want to provide an implementation manually & instead want to make use of the method already available for addition.

We want to reuse the existing method.

This is when "*Method Reference*" comes into the picture.

To reference a static method, we have to use a double colon i.e. "**::**".

<img width="669" alt="Screenshot 2024-07-28 at 10 48 11 PM" src="https://github.com/user-attachments/assets/2da6611e-93df-45da-9660-27553536bcd1">
<img width="996" alt="Screenshot 2024-07-28 at 10 49 09 PM" src="https://github.com/user-attachments/assets/5b5a7af4-7707-49d4-b6be-93b3ebfe6877">

# JAVA Method Reference

Method Reference is nothing but reusing something that already exists in the code base.

<img width="1191" alt="Screenshot 2024-07-28 at 10 51 31 PM" src="https://github.com/user-attachments/assets/aebc9aed-b80f-4b94-af52-c0df51b9f8cd">

1. ### Static method:

   We have an inbuilt class called "Integer". It has a static method named "*sum()*".

   <img width="735" alt="Screenshot 2024-07-28 at 10 53 41 PM" src="https://github.com/user-attachments/assets/27dc37d1-3e0e-48d9-8883-d3aaa2a7f71e">

   This would be a perfect fit for our sum method implementation. We can refer to the same. Also, we don't need to pass parameters.

   <img width="1038" alt="Screenshot 2024-07-28 at 10 55 32 PM" src="https://github.com/user-attachments/assets/968b0b69-0b72-408d-aca6-e222fd20dd1c">

   Its equivalent lambda expression is,

   <img width="740" alt="Screenshot 2024-07-28 at 10 57 49 PM" src="https://github.com/user-attachments/assets/5554e7bb-2c55-4ecb-9bcd-b7812b63573a">

   Let's say we want to sort a list of integers. We have a Function Interface "ISort".

   <img width="979" alt="Screenshot 2024-07-28 at 10 59 31 PM" src="https://github.com/user-attachments/assets/24a2a305-ad0c-45aa-8dc6-92dbea045ae2">

   We can have a lambda expression for the same.

   <img width="743" alt="Screenshot 2024-07-28 at 11 01 32 PM" src="https://github.com/user-attachments/assets/9857b9bf-0e89-467d-be07-4dc031d8fdbc">

   We are actually not doing anything or providing the implementation. We are simply calling the "Collection.sort()" method and using it to sort.
   So, we can refer to that method directly instead.

   <img width="1018" alt="Screenshot 2024-07-28 at 11 03 34 PM" src="https://github.com/user-attachments/assets/36e52376-c495-4ecd-830f-dc1bf0b52d0d">
   <img width="1206" alt="Screenshot 2024-07-28 at 11 04 26 PM" src="https://github.com/user-attachments/assets/4bbe05a5-c81e-4466-8ae7-fb5e59e30402">

   ### Does that mean any method can be used for method reference?

   Consider a Functional Interface "IPrint".

   <img width="825" alt="Screenshot 2024-07-28 at 11 06 01 PM" src="https://github.com/user-attachments/assets/45669206-b092-4c14-aaf8-7738e3d3195a">

   We need to provide an implementation.

   <img width="930" alt="Screenshot 2024-07-28 at 11 06 48 PM" src="https://github.com/user-attachments/assets/d1ee92a1-ed57-4e4a-9684-580ef5ff0cf6">

   We want to wrap up the same logic inside a method and then use it.

   <img width="661" alt="Screenshot 2024-07-28 at 11 10 08 PM" src="https://github.com/user-attachments/assets/a4e7d39a-4c93-4c72-8ef6-667ac35f7037">

   But suppose the referenced method's return type is changed.

   <img width="722" alt="Screenshot 2024-07-28 at 11 11 11 PM" src="https://github.com/user-attachments/assets/a3f48ded-a960-48a7-b44c-5157ed49314c">

   ### But will our method referencing work?

   It shouldn't ideally. But it works fine.

   <img width="889" alt="Screenshot 2024-07-28 at 11 11 25 PM" src="https://github.com/user-attachments/assets/f56b559d-665d-493b-adf7-a60eefe88e18">

   We actually need to just take care of method arguments and not the return type. But if our abstract method returns something, then return type of
   the method we are reusing should match.

   
   

   
   
   























  
