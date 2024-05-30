# **Spring Mvc Data Binding**

* Create a sample Controller

  <img width="973" alt="Screenshot 2024-05-30 at 5 24 25 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/68bf8cbd-5ec6-4f4d-b12f-f22a88c815c3">
  <img width="986" alt="Screenshot 2024-05-30 at 5 24 36 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/09287f96-08dd-478a-8b42-cfb804961e06">

  home-page.jsp

  <img width="988" alt="Screenshot 2024-05-30 at 5 27 04 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/f159214c-5e31-4a6f-a06d-ffb48b662ed2">

  Run the application

  <img width="862" alt="Screenshot 2024-05-30 at 5 25 44 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/fcc72043-a379-4c50-8957-bf564192e956">
 
  When we enter details and hit calculate

  <img width="556" alt="Screenshot 2024-05-30 at 5 29 17 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/eb2b5df9-bb1b-4bcc-9e66-e49286285c1d">

      http://localhost:8080/Spring-love-calculator/process-homepage?username=Sheldon&crushName=Amy
  
  Let's analyse. All the information that is entered is Query String.

  <img width="653" alt="Screenshot 2024-05-30 at 5 32 20 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/623f5fc2-1bd4-4ca7-aa20-4d6281ddebaf">

* Data Binding(Capture user data): We can use @RequestParam to extract query parameters, form parameters, and even files from the request. Using RequestParam,
  we can actually bind the values.

  <img width="920" alt="Screenshot 2024-05-30 at 5 59 21 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/525dc1ee-b322-4680-ab38-4dbd133d8290">

  Can also be written as,

  <img width="713" alt="Screenshot 2024-05-30 at 5 58 10 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/2e031123-6218-4fb9-bb97-29ff5335a76b">

  To send data from Controller to view, we can use Model.

  <img width="970" alt="Screenshot 2024-05-30 at 6 07 36 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/4f664ad4-4977-464c-b791-8c2a256afae4">

  However, if there are multiple such queryParams, it will become very difficult manage all using RequestParam for each.
  Spring provides a standard way to do Data Binding. (DTO - Data Transfer Object). It automatically binds form data with dto(pojo).
  **Note:** Form parameter name should match the variable names.

  <img width="1092" alt="Screenshot 2024-05-30 at 6 32 50 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/4ec0cf12-1c68-49dd-8374-d4fd31946bd3">
  <img width="1119" alt="Screenshot 2024-05-30 at 6 35 28 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/fcee596b-101e-48dc-8363-f0fa357cbe61">
  <img width="1119" alt="Screenshot 2024-05-30 at 6 35 57 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/3f4fbba7-48a0-4e34-a8ea-cdf46de4554f">

  <img width="925" alt="Screenshot 2024-05-30 at 6 12 00 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/041ee619-aa72-4cbb-87e7-492744acb48a">
  <img width="968" alt="Screenshot 2024-05-30 at 6 33 05 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/a7bfb06a-c00f-40ad-92ea-03e8d1aa6ab5">
  <img width="851" alt="Screenshot 2024-05-30 at 6 33 14 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/c4329cfd-1722-4b7f-bd7d-235875b6dd9c">
  <img width="951" alt="Screenshot 2024-05-30 at 6 33 39 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/d0f14249-3798-466c-bf2a-f89f38cb70ed">

* Spring Mvc form tag:

  <img width="1027" alt="Screenshot 2024-05-30 at 7 06 19 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/aa941c08-ff06-4344-b844-7c49647d6a34">
  <img width="1211" alt="Screenshot 2024-05-30 at 7 06 42 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/4664e6f4-cf73-443c-bb9b-4911b4287b88">
  <img width="1115" alt="Screenshot 2024-05-30 at 7 06 54 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b166ae7b-5fe5-451c-b188-18c8589a73c5">
  <img width="1141" alt="Screenshot 2024-05-30 at 7 09 39 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/03077bba-a439-494c-971c-840eb3cad824">
  <img width="1097" alt="Screenshot 2024-05-30 at 7 39 08 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/8d8d4f19-5181-4242-ae5d-4d351513b0b3">

  We can add default values to properties

  <img width="635" alt="Screenshot 2024-05-30 at 7 30 21 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/f5000899-5d6b-45bb-bee1-b0d30cdbbf1f">
  <img width="960" alt="Screenshot 2024-05-30 at 7 23 38 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/e8b6087c-efa4-4fa4-945d-25c6993d8ece">

  To be able to use it, add attribute to the Model

  <img width="970" alt="Screenshot 2024-05-30 at 7 25 54 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/3cce8d31-af63-457d-811f-653e42b16a31">

  Use spring mvc form tag (Remember to add taglib),

  <img width="960" alt="Screenshot 2024-05-30 at 7 26 26 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/8648f184-fcf0-491f-92c2-a1c0587c78d2">
  <img width="808" alt="Screenshot 2024-05-30 at 7 16 31 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/131ba7be-6784-48d5-a883-fedc5c62733b">

  We can directly make use of @ModelAttribute as well,

  <img width="966" alt="Screenshot 2024-05-30 at 7 31 48 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/88176ace-6ad6-4cbc-a780-9b7f69843530">
  <img width="968" alt="Screenshot 2024-05-30 at 7 32 31 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/efc084f8-66f2-495e-8cf9-14947e58863d">
  <img width="925" alt="Screenshot 2024-05-30 at 7 32 53 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/6e33e7e7-1176-4a49-b02c-d0e885d04337">

  <img width="635" alt="Screenshot 2024-05-30 at 7 30 21 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/6b3a2545-ec44-4f6d-a526-2e9af1b2c7c7">
  <img width="654" alt="Screenshot 2024-05-30 at 7 30 42 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/bb5ccb64-8f3c-41f7-abbf-af26e0cf64bf">
  <img width="677" alt="Screenshot 2024-05-30 at 7 30 51 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b56d9ec1-636c-4f66-a29f-bfd61157cc1c">


  
  

  



