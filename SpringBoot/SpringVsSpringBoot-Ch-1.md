# Why SpringBoot?

Let's try to create a simple Hello World application first with Raw Spring Framework and then with SpringBoot. We can then compare the two.

## 1. With Raw Spring Framework

   <img width="1137" alt="Screenshot 2024-06-20 at 7 55 51 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c1fa933a-7b72-46ea-ac59-4ba68f9ed0f1">
   <img width="745" alt="Screenshot 2024-06-20 at 7 56 01 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7ddaf7b0-53fe-46b3-b32b-66b346da8bb7">
   <img width="387" alt="Screenshot 2024-06-20 at 8 04 09 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/217c1946-1b6d-4919-b75a-a3bc7c9f4da3">
   <img width="790" alt="Screenshot 2024-06-20 at 8 12 38 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d3948972-1ce7-4ab0-bc22-f92fe96ed497">
   <img width="421" alt="Screenshot 2024-06-20 at 8 09 33 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ff3087c6-5498-43e7-9c36-c7233f4ac1ab">
   <img width="852" alt="Screenshot 2024-06-20 at 8 12 48 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/31f95333-7a42-44f7-9476-db3496aeb05a">
   <img width="927" alt="Screenshot 2024-06-20 at 8 47 55 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ef2fd856-b5da-495b-989a-bdd312d4a891">

   Run the Application on Tomcat Server

   <img width="655" alt="Screenshot 2024-06-20 at 8 20 09 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/fc6a2fa3-6ea2-4d62-97d3-e172cd00b738">

   We can see even a simple Hello world Application needs some effort and strong foundation. We need to configure a DispatcherServlet and a Configuration File.

   Before that, let's try to understand few concepts,
   
   <img width="881" alt="Screenshot 2024-06-20 at 8 22 01 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/6ef4d272-a52a-4d63-8537-d967be12cf96">
   <img width="1198" alt="Screenshot 2024-06-20 at 8 24 13 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/56c12eb6-6199-40c6-9b4c-58eb5ab242af">
   <img width="1175" alt="Screenshot 2024-06-20 at 8 24 34 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/835726e4-3963-43c1-8ed9-e870843caaf3">
   <img width="1090" alt="Screenshot 2024-06-20 at 8 25 01 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/f2945ced-9645-4979-b1f7-fa2160bb3248">
   <img width="1027" alt="Screenshot 2024-06-20 at 8 25 54 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/e33a90e0-aa24-4f2e-955b-4db72bdf40ae">
   <img width="846" alt="Screenshot 2024-06-20 at 8 26 12 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/42f53cdb-03f9-4e75-9f1d-cc25d5cfcd42">
   <img width="1079" alt="Screenshot 2024-06-20 at 8 26 41 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/cd5fc370-7505-48ca-a718-1ca57f673bd7">
   <img width="766" alt="Screenshot 2024-06-20 at 8 28 01 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/00c81a17-8767-4518-8b7e-d1bc5c134fd9">
   <img width="772" alt="Screenshot 2024-06-20 at 8 28 18 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/85f295ee-e843-4d14-ae1d-c5e8013bc265">
   <img width="906" alt="Screenshot 2024-06-20 at 8 28 33 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/f21afc29-edd7-4173-b4cb-59676778fbf9">
   <img width="986" alt="Screenshot 2024-06-20 at 8 29 05 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/27834279-d8ee-4b65-a605-b767f2827232">
   <img width="1209" alt="Screenshot 2024-06-20 at 8 29 21 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9e2ac824-0d2e-4dba-b489-ef9c1be12920">
   <img width="1114" alt="Screenshot 2024-06-20 at 8 30 00 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/721397c1-8b95-4625-b7ad-14ca62b19e98">
   <img width="1131" alt="Screenshot 2024-06-20 at 8 30 30 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9b74b35d-72a9-4715-9ea7-f89549071a18">
   <img width="1270" alt="Screenshot 2024-06-20 at 8 31 04 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8cb3815e-e010-43a5-a863-5c0155f2d016">
   <img width="1115" alt="Screenshot 2024-06-20 at 8 31 36 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/376eb119-185c-45b0-9a13-67f82f462caf">
   <img width="594" alt="Screenshot 2024-06-20 at 8 32 28 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/0a0221c3-0508-4936-9188-4df7817570fa">
   <img width="1101" alt="Screenshot 2024-06-20 at 8 33 35 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/6ca68ebe-dacd-4091-a4c2-359b2c717d07">

   We need to create a DispatcherServlet and a Configuration File

   <img width="392" alt="Screenshot 2024-06-20 at 8 35 02 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8f77386f-6a42-490d-8405-b73df893d03c">
   <img width="779" alt="Screenshot 2024-06-20 at 8 40 48 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/e766b5c0-be9f-4e65-87ad-1bc97798dd38">
   <img width="375" alt="Screenshot 2024-06-20 at 8 40 40 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8feaf5db-0a85-4915-bf46-43a540f0f0f0">

   Spring will use the below to setup DispatcherServlet

   <img width="983" alt="Screenshot 2024-06-20 at 8 46 14 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/03367a7b-0881-4e2e-a52c-b42c294e5540">

   Run the Application

   <img width="707" alt="Screenshot 2024-06-20 at 8 49 28 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/34b6cd2f-ee4d-4642-9bfa-5706b293ef13">
   <img width="974" alt="Screenshot 2024-06-20 at 8 49 33 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/97606ff0-8edb-41e9-a812-dcc261190370">

   We had to do so much of Configuration to build a simple hello world application.

   #### Note: We can use *@RestController* as well instead of @Controller and @ResponseBody. This is because RestController already has Controller and ResponseBody.

   <img width="869" alt="Screenshot 2024-06-20 at 10 23 41 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/358b2662-239f-4123-8559-57eff8bf4d76">
   <img width="576" alt="Screenshot 2024-06-20 at 10 27 00 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/85c5a4ee-676b-4634-b0a1-96d297fb4419">

## 2. With SpringBoot

   <img width="895" alt="Screenshot 2024-06-20 at 8 52 08 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/0e48adbe-521e-4c04-a9ef-55f5217a052c">

   Go to https://start.spring.io/, add spring web mvc dependency and generate the project.

   <img width="1320" alt="Screenshot 2024-06-20 at 8 55 52 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d70f0ec6-57d2-4fda-8e97-5c478c56bab1">

   There is a SpringBoot generated file already present

   <img width="784" alt="Screenshot 2024-06-20 at 10 07 41 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c6c09971-500a-46de-aace-a21f2dcf89ad">

   Create a Controller

   <img width="849" alt="Screenshot 2024-06-20 at 10 07 01 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/bca2b69f-a4b1-4e8b-9f31-12783e73b5a4">

   Run the Application

   <img width="1351" alt="Screenshot 2024-06-20 at 10 10 27 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/bbd50ef1-47ee-46c1-b665-aabe550b9561">

   Go to localhost port 8080

   <img width="1098" alt="Screenshot 2024-06-20 at 10 10 34 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/77f42c6c-f9fb-42ad-a6b3-529332fc963f">

   We can see how easy it is to create and run a simple Hello World SpringBoot project. We didn't have to do any configuration at all. We didn't have to spend any time in setting up 
   our project.

### FYI

<img width="1101" alt="Screenshot 2024-06-20 at 8 01 48 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9695c415-f6f5-44c3-b12f-1b2f443d7c3b">
<img width="785" alt="Screenshot 2024-06-20 at 8 01 53 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/bb331f43-524b-469a-92b7-7d865910d835">

#### Compatibility

<img width="268" alt="Screenshot 2024-06-20 at 8 18 42 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/4185b5ca-43c7-45bc-9b72-e8b62a9755e0">
<img width="292" alt="Screenshot 2024-06-20 at 8 18 52 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/37b9cee4-b53b-4f97-8edf-2f43f0337957">
