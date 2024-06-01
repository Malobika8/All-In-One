# **Spring MVC Formatter**

* DataBinding for nested objects:

  <img width="904" alt="Screenshot 2024-06-01 at 9 45 30 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/f5a945b0-6c52-4ae3-8df8-4a4a0f465be3">
  <img width="803" alt="Screenshot 2024-06-01 at 9 46 33 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/7e90bb96-046a-496c-bebb-8fb8c8f73a40">
  <img width="997" alt="Screenshot 2024-06-01 at 9 46 20 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/bb4544d4-6b97-4ec0-b239-46d4d7907505">
  <img width="1440" alt="Screenshot 2024-06-01 at 9 47 32 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/18bbd446-3b96-4d9c-9d69-7e62d3391dc2">
  <img width="802" alt="Screenshot 2024-06-01 at 9 47 54 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/ecf6b61c-d432-4d21-b748-44547d742f52">
  <img width="1169" alt="Screenshot 2024-06-01 at 9 47 43 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b63992db-e00a-45bc-a0fb-776178bb3780">
  <img width="1138" alt="Screenshot 2024-06-01 at 9 48 58 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/26459a14-18ca-4d31-a9f6-95a538dcff4a">
  <img width="1135" alt="Screenshot 2024-06-01 at 9 49 12 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/33cce444-3836-4ccd-9048-84705689c47b">
  <img width="1147" alt="Screenshot 2024-06-01 at 9 49 27 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/cc496b35-5c20-4c69-a027-f6771434e1eb">
  <img width="965" alt="Screenshot 2024-06-01 at 9 57 07 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/cabeee56-e905-4741-95ba-9797ecef4541">

  Run the application
  <img width="1197" alt="Screenshot 2024-06-01 at 9 55 31 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/cadf9a73-a1c7-4af9-946b-b5fed46086e6">

  <img width="922" alt="Screenshot 2024-06-01 at 9 58 23 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/968c048a-0f6b-4a35-9a4a-d254fa912b0b">
  <img width="1147" alt="Screenshot 2024-06-01 at 10 01 28 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/991a7f69-e1f5-48f3-a560-b1b2be8c3082">
  <img width="756" alt="Screenshot 2024-06-01 at 10 07 01 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/690f4696-0c47-424d-9970-9fe6e7bdd691">
  <img width="964" alt="Screenshot 2024-06-01 at 10 07 21 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/084d0c5b-f014-481b-a012-c87f029572a2">

  *When we run the application, we get 400-BadRequest. Why so?*

  <img width="1074" alt="Screenshot 2024-06-01 at 10 08 47 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/e41d07e1-a8b4-4eb8-8a7e-f4273de047d2">

  This is because Spring is not able to bind the nested Phone object as it doesn't know the data type. In such cases, we need to use formatter.

* Formatter:
  
  **How to write a formatter to help Spring in Data Binding when dealing with special kind of objects like phone, credit card etc.?**

  We can utilize the Formatter Interface.

  <img width="1130" alt="Screenshot 2024-06-01 at 10 50 54 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/9a50d350-5e8d-41c8-902d-86fcd13fded5">
  
  We need to let Spring know that we are using a Formatter by implementing WebMvcConfigurer in Spring Config. WebMvcConfugirer has addFormatter
  method. This formatter helps in DataBinding.

  <img width="977" alt="Screenshot 2024-06-01 at 10 55 57 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/ee835307-07fe-4aed-b7f2-51d8b5c46684">
  <img width="977" alt="Screenshot 2024-06-01 at 11 11 58 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/cb00d261-b107-4e98-a607-e9716ac4088d">
  <img width="1027" alt="Screenshot 2024-06-01 at 11 12 24 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/048414dd-391c-4e3b-b9f6-c671484b2245">

  Run the application

  <img width="1301" alt="Screenshot 2024-06-01 at 11 13 50 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/9116be6d-0152-4ccd-9654-116930585380">
  <img width="1091" alt="Screenshot 2024-06-01 at 11 13 41 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/3c43a22a-e897-4861-82af-d3820d4915c8">

  To show default phone number on the UI
  
  <img width="788" alt="Screenshot 2024-06-01 at 11 16 03 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/d1029ae1-c6c1-427a-b3cd-06a53beecd62">
  <img width="675" alt="Screenshot 2024-06-01 at 11 17 19 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/9229975a-d751-4ac0-8267-64e84f6286ab">
  <img width="1061" alt="Screenshot 2024-06-01 at 12 13 08 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/f1eddc42-68ea-4286-8028-24a06ef5cecb">
  <img width="889" alt="Screenshot 2024-06-01 at 12 13 28 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b9a62f04-bc4c-43b4-b5ed-f7f51594e62a">

  Run the application

  <img width="1218" alt="Screenshot 2024-06-01 at 12 14 24 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b4341f53-e4f6-40c3-898c-7bb55dc34575">

* Minor improvements:

  
  
  

