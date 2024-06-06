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
<img width="1404" alt="Screenshot 2024-06-06 at 12 49 58 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/8711e248-03b2-4ace-bafc-b5685c89c5ae">
<img width="1086" alt="Screenshot 2024-06-05 at 10 16 24 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/3e28f967-c1f3-4c56-976c-e5083e413ee5">
<img width="1056" alt="Screenshot 2024-06-05 at 10 17 30 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/33862029-de7c-4a2b-bad8-714ce13e0cb7">

Add validator in InitBinder.

<img width="1044" alt="Screenshot 2024-06-05 at 10 30 11 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b24da3e1-54c7-4050-a457-3613e217371d">

Run the application and it should work fine.

<img width="1012" alt="Screenshot 2024-06-05 at 10 37 38 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/9c29419e-71b7-4798-bff3-56e1bdf37160">
<img width="1068" alt="Screenshot 2024-06-05 at 10 38 23 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/c5fc423c-5658-4efa-8fbb-a8703cbc9e0a">
<img width="1256" alt="Screenshot 2024-06-06 at 12 50 55 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/236f78e2-65bb-490b-a616-ddcb777557b7">

The Spring validators can be manually called as well.

<img width="1072" alt="Screenshot 2024-06-06 at 12 54 43 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/17802c7f-fb01-4b8b-91d9-fe4351f63cd9">

We can let Spring create an object of validator using @Component & @Autowired

<img width="1047" alt="Screenshot 2024-06-06 at 12 57 22 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/885370f3-3063-4e71-8179-6edc0311b32b">
<img width="1091" alt="Screenshot 2024-06-06 at 12 57 36 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/ade6115b-e914-4a32-b11b-b415b216def5">
<img width="776" alt="Screenshot 2024-06-06 at 12 59 25 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/23097b5b-837e-4bf0-8e2a-e6498bc008a3">

OR

<img width="735" alt="Screenshot 2024-06-06 at 1 01 36 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/34ec0cf0-10c3-4f1a-9960-db302541dfb1">

### Extra

To use variable name in properties file

<img width="742" alt="Screenshot 2024-06-06 at 1 05 13 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/67943aed-44ba-46c9-af52-9fe4d8efd6c0">
<img width="738" alt="Screenshot 2024-06-06 at 1 07 33 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/efea0386-02b8-4691-b7e8-502e7ec4b7c6">
<img width="606" alt="Screenshot 2024-06-06 at 1 07 49 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/1f162caf-7307-4e47-bdff-c60e94b17cda">

We can modify error msgs as well. Suppose while filling age, we provide String instead of int, we can control and display custom message instead of NumberFormatException on UI.

<img width="1075" alt="Screenshot 2024-06-06 at 1 17 09 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/783b7ee5-b65a-4e6e-965d-54a8097318e6">
<img width="1076" alt="Screenshot 2024-06-06 at 1 17 40 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/a763df20-528c-432c-987d-8aa537bef982">
<img width="1067" alt="Screenshot 2024-06-06 at 1 15 20 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/a0116d14-d71f-425f-979f-270e6da57d8a">


