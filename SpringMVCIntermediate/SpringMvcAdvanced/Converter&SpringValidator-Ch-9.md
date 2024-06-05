*What is a Converter? - These are like an alternative to PropertyEditor.*

Create a CreditCardConverter class. It should implement Converter<S,T> and overwrite convert method.

<img width="1373" alt="Screenshot 2024-06-05 at 9 54 39 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/2797c903-6add-4bee-9dac-7b3d45b8ad08">

We need to add Converter in Config class.

<img width="1094" alt="Screenshot 2024-06-05 at 9 55 21 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/23b02cf3-d9fa-4af1-9615-272081cb0829">

Note that there's no alternative method present as print(in Formatter) or getAsText(in PropertyEditor). So everytime, we want to prepopulate 
the field with some sample data, we would require to create a new converter class but interchanging source.

<img width="812" alt="Screenshot 2024-06-05 at 9 50 25 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/6eeaddbe-3d4b-4e65-b39b-32f6bc0b201a">


# Spring Validators

<img width="1118" alt="Screenshot 2024-06-05 at 9 58 19 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b457cdaf-a539-4616-875c-dc6649635401">

Consider a scenario where during registration username cannot be empty and should contain '-'. We need to use a custom Validator without using jsr
specification.

Create a new UserNameValidator. It should implement Validator class(spring Validator).

<img width="935" alt="Screenshot 2024-06-05 at 10 17 54 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/4e059d16-7dcb-460c-9b92-c19110a53ad4">
<img width="1371" alt="Screenshot 2024-06-05 at 10 36 47 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/80ece931-3033-47d0-9d58-ff0b6dfa2a3e">
<img width="1086" alt="Screenshot 2024-06-05 at 10 16 24 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/3e28f967-c1f3-4c56-976c-e5083e413ee5">
<img width="1056" alt="Screenshot 2024-06-05 at 10 17 30 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/33862029-de7c-4a2b-bad8-714ce13e0cb7">

Add validator in InitBinder.

<img width="1044" alt="Screenshot 2024-06-05 at 10 30 11 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b24da3e1-54c7-4050-a457-3613e217371d">

Run the application and it should work fine.

<img width="1012" alt="Screenshot 2024-06-05 at 10 37 38 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/9c29419e-71b7-4798-bff3-56e1bdf37160">
<img width="1068" alt="Screenshot 2024-06-05 at 10 38 23 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/c5fc423c-5658-4efa-8fbb-a8703cbc9e0a">
