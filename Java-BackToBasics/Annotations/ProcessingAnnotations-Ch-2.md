# Process annotation for Class

We have "*myCat*" object that is an instance of the "*Cat*" class annotated.

We can check if the Class is annotated with *@VeryImportant* annotation.

<img width="994" alt="Screenshot 2024-07-26 at 12 37 31 PM" src="https://github.com/user-attachments/assets/61012c1d-7a5b-4351-8cfb-2acba4aa3a55">

## Let's create & process Custom Annotation for methods

<img width="868" alt="Screenshot 2024-07-26 at 12 40 19 PM" src="https://github.com/user-attachments/assets/86554f83-1aac-44af-a2d6-d2e0b4096b7b">
<img width="857" alt="Screenshot 2024-07-26 at 12 40 29 PM" src="https://github.com/user-attachments/assets/ed4374c7-cb79-4447-8868-c692c52fb98a">

Run immediately if *@RunImmediately* annotation is present.

<img width="996" alt="Screenshot 2024-07-26 at 12 42 05 PM" src="https://github.com/user-attachments/assets/bba5e331-9c6f-444b-a24f-e5ca0732b37e">

It called the "*meow()*" method and not the "*eat()*" method.

<img width="1063" alt="Screenshot 2024-07-26 at 12 42 29 PM" src="https://github.com/user-attachments/assets/88648619-7e19-4917-b449-86cab6cf8ebe">

We can add our own parameters to our custom annotations. Suppose we want to  have parameter for the number of times the method should run.
In the body of the Custom Annotation class, we need to add the parameter as method(and not a normal class field).

<img width="852" alt="Screenshot 2024-07-26 at 12 44 03 PM" src="https://github.com/user-attachments/assets/f20cb604-657d-4038-abbe-c4d08d5f78ab">
<img width="857" alt="Screenshot 2024-07-26 at 12 47 49 PM" src="https://github.com/user-attachments/assets/f3c7c867-bc00-4be1-a6f3-5d608ebad581">
<img width="1028" alt="Screenshot 2024-07-26 at 12 49 09 PM" src="https://github.com/user-attachments/assets/fb36c83c-891f-4c0a-8642-b2e487e0a425">
<img width="1066" alt="Screenshot 2024-07-26 at 12 49 54 PM" src="https://github.com/user-attachments/assets/264492a7-ab44-4e1c-bb1b-cabc6d87816b">

There are a few things to note about these parameters
- We cannot use just any type we want for these parameters. They can only be a primitive type, a class type, a String or an array of any of those.
- We can add default values if we want to.

  <img width="1039" alt="Screenshot 2024-07-26 at 12 52 32 PM" src="https://github.com/user-attachments/assets/a2616a8b-ec5b-4fe0-8e29-fd47f62ef3fd">

## Let's create & process Custom Annotation for a field in a Class

<img width="942" alt="Screenshot 2024-07-26 at 12 54 29 PM" src="https://github.com/user-attachments/assets/e57c5c53-2174-4eab-87f9-070978bfded3">
<img width="942" alt="Screenshot 2024-07-26 at 12 54 29 PM" src="https://github.com/user-attachments/assets/dd54d264-3870-4c43-8c4f-2e6563304673">
<img width="838" alt="Screenshot 2024-07-26 at 12 55 17 PM" src="https://github.com/user-attachments/assets/5fe7f69d-fb3f-4522-8e26-4c2287ce6a34">

Suppose we want the Annotation to be used only over String fields.

<img width="1011" alt="Screenshot 2024-07-26 at 12 57 45 PM" src="https://github.com/user-attachments/assets/4e4dd4f9-4259-4df6-8605-f6aedb5e3a91">
<img width="840" alt="Screenshot 2024-07-26 at 12 57 56 PM" src="https://github.com/user-attachments/assets/f6f9a304-8039-4e23-aa25-6e78eabb88d1">

