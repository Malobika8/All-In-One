## Design email Controller and email View

* Create EmailDTO

  <img width="930" alt="Screenshot 2024-06-13 at 12 07 36 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/1790baa6-60dc-4685-8b8c-ff65e639bf50">

* Create EmailController

  <img width="985" alt="Screenshot 2024-06-13 at 12 07 56 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/75a19bd2-d46b-402e-8939-5170413d5b1f">

* Update/Create jsp pages

  <img width="1056" alt="Screenshot 2024-06-13 at 12 08 46 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/fc421dc4-0833-44a6-a200-6ec1c2ea3450">
  <img width="958" alt="Screenshot 2024-06-13 at 12 09 05 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b36e62b9-131b-4db3-ae3a-6f0049fa495e">
  <img width="801" alt="Screenshot 2024-06-13 at 12 09 12 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a4b4918c-ef6f-4f13-9575-65c3d4022cd8">

* Run the Application

  <img width="663" alt="Screenshot 2024-06-13 at 12 10 16 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9ab060d4-90a4-478a-b156-c1e9f1946690">
  <img width="723" alt="Screenshot 2024-06-13 at 12 10 21 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/fbe8abc1-8562-4124-a500-4e731d3ca05f">
  <img width="745" alt="Screenshot 2024-06-13 at 12 10 45 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/41df656c-982e-449e-a5fe-feeebae05b57">
  <img width="713" alt="Screenshot 2024-06-13 at 12 10 50 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/bbf26481-8853-4a0a-aeba-21b2756ab348">

## How to retain some data throughout the session?

The model object is used to transfer data to a page. However, once the data is fetched and showed to user, the model object is destroyed.

<img width="1087" alt="Screenshot 2024-06-14 at 10 30 09 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/077157ea-244c-468e-8dab-f9d7e00082d8">

*The easiest way is to send the data through URL.*

<img width="896" alt="Screenshot 2024-06-14 at 10 35 38 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b09ff269-50d1-4d6f-8dcf-6fc2fc305b28">
<img width="936" alt="Screenshot 2024-06-14 at 10 36 34 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7b206312-b660-42c4-a6f2-fbb86453c8ae">

<img width="1106" alt="Screenshot 2024-06-14 at 10 37 51 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/0912417d-bf3b-4c5f-b500-2fdcfde09cab">

We can set a query String,

<img width="1056" alt="Screenshot 2024-06-14 at 10 39 16 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/94524676-2f00-42ca-995d-0f16d8e9d8af">
<img width="813" alt="Screenshot 2024-06-14 at 10 40 38 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/84e01f02-4c64-422a-9b8c-977e96a8dded">
<img width="747" alt="Screenshot 2024-06-14 at 10 41 10 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9956d0d9-e93d-4e7b-8b2d-f6c99af5e072">

We can then pass it to the next page through a model/model-attribute.

However, we do not want to use query param.

<img width="894" alt="Screenshot 2024-06-14 at 10 43 18 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/5facbcc0-90f6-43a4-bdc0-6dfe41d5b418">

## Path Variable

<img width="1077" alt="Screenshot 2024-06-14 at 10 46 24 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/e0b8db31-40a0-4e4b-a033-d1255fcc61e9">

Note: Forgot to add '$'

<img width="1056" alt="Screenshot 2024-06-14 at 10 47 32 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/538fc2ac-02ba-49e4-bf18-8b6fdbedb0fa">

Run the Application

<img width="838" alt="Screenshot 2024-06-14 at 10 55 03 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/f74f1b91-1b68-485a-a288-8ba1f1d553ca">
<img width="852" alt="Screenshot 2024-06-14 at 10 55 16 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/65ac885a-46a6-485d-b891-8b86fadcb6eb">

<img width="1278" alt="Screenshot 2024-06-14 at 10 57 02 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/882568f8-79fc-4653-b766-db888f67d1a6">
<img width="639" alt="Screenshot 2024-06-14 at 10 57 15 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/fb241b44-1070-4439-8bdf-907392eebe1a">
<img width="745" alt="Screenshot 2024-06-14 at 10 58 41 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/526b23d1-4dc4-4688-a233-90fb9f8e349c">
<img width="604" alt="Screenshot 2024-06-14 at 10 58 03 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/4855397a-b06a-434c-97f0-314cc6ffcade">

## Why we should not transfer data through URL?

- We would need to attach the data to multiple urls so that it is accessible in multiple pages. With this, we would need to handle the same 
  in multiple handler methods. If suppose we have hundred pages where we require the same data, it's practically not feasible to keep on
  forwarding the data in such manner.
- The same url can be reused to display the page. Transferring data through URLs in Spring can be insecure as the data is visible to anyone 
  who has access to the URL. Malicious actors can intercept and read the data or modify it, resulting in data breaches. 

<img width="1136" alt="Screenshot 2024-06-14 at 11 07 22 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/fbc4953b-0361-4498-b8bb-716ab862df3a">

We can do that using **Session**.
