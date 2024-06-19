# Cookies

Say we have a Client and a Server. We establish a Connection and a Request goes to the Server. It will process and send back a particular response. Once done, the connection will be dropped since Http is a stateless protocol.

That means once we connnect to the Server and get a Response back, the Request and Response objects will be destroyed. Next time if we connect to the Server, that will be a new Request the Server will be receiving and Server won't be knowing who is sending the Request.

When we send a Request, a file called Cookie is created where all relevant info is stored and with Response it sends the cookie as well to the client's computer.

Next time, when we send a Request, along with it, saved Cookie is also sent which is then used by the Server to personalize the Response.

## What are Cookies?
Cookies are small text files that are stored on your device when you visit a website. These files contain information about your preferences, your browsing session, and other data that can help websites personalize your experience and provide you with relevant content. Cookies are considered an essential part of the internet ecosystem, as they allow websites to provide features such as authentication, shopping carts, and analytics. However, they can also be used by hackers to steal personal information and data, which is why it's important for you to know what cookies are and how to manage them.  

*How to store UserName with Cookie?*

<img width="1037" alt="Screenshot 2024-06-18 at 10 15 37 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a2037718-a442-48a1-b543-d742ee781e4e">


<img width="1429" alt="Screenshot 2024-06-15 at 10 46 22 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9eae8d8b-938c-4e1d-bdad-10b2c38b69fd">
<img width="1440" alt="Screenshot 2024-06-15 at 10 46 58 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/365d8da1-13e4-48c2-9e45-66e314f07873">
<img width="1169" alt="Screenshot 2024-06-15 at 10 49 35 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/31a03d98-f17a-4ae3-a4ad-360b449f1076">
<img width="1161" alt="Screenshot 2024-06-15 at 10 49 41 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/956fd601-ec34-4e25-b085-5391102a1bca">
<img width="1115" alt="Screenshot 2024-06-18 at 10 37 43 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/63312c9a-b9d5-482d-bbc9-f484b22f0f0d">
<img width="793" alt="Screenshot 2024-06-18 at 10 38 01 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/e99cb935-487c-4e6a-95a7-f5b62843365e">
<img width="800" alt="Screenshot 2024-06-18 at 10 38 12 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/1de3f35a-8ad6-49c2-8d1f-e875649304fa">
<img width="971" alt="Screenshot 2024-06-18 at 10 38 18 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/84cc9f6d-e9b6-4836-8352-471c59384684">

Different browsers are considered as different Clients.

## Reuse Cookie info to pre-populate UserName if the User has already visited the Website previously in the same browser

<img width="788" alt="Screenshot 2024-06-18 at 10 42 57 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c0118d09-72ab-432f-adf8-3c54984e904f">
<img width="942" alt="Screenshot 2024-06-18 at 10 48 48 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/038a0c10-fe40-4c92-b71f-53d2b76d5c08">
<img width="831" alt="Screenshot 2024-06-18 at 10 48 58 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d0010cec-921a-4ec2-91be-0cbe57973fd9">
<img width="731" alt="Screenshot 2024-06-18 at 10 49 11 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/116210f2-0a81-49dc-b100-989be8df606d">

## Reading Cookies using Spring

<img width="695" alt="Screenshot 2024-06-18 at 11 03 44 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/76fd883b-968c-47be-a489-b03741394333">
<img width="1075" alt="Screenshot 2024-06-18 at 11 06 34 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/be9a92a6-74d9-493d-af36-f70405bea73c">
<img width="993" alt="Screenshot 2024-06-18 at 11 07 16 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d3fa92cf-f150-4cac-a68f-2fe30a6134d5">
<img width="1104" alt="Screenshot 2024-06-18 at 11 07 58 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d315f5bd-ebd7-4540-a71b-5426341b3cce">

Able to populate name from Cookie

<img width="1054" alt="Screenshot 2024-06-18 at 11 08 05 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b15e2026-c65a-43e8-b774-85f334fb2cf8">


## Disadvantages of using Cookies

<img width="937" alt="Screenshot 2024-06-18 at 11 09 59 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/3336664a-fc08-40df-a61e-8f08b4caaf1d">
<img width="951" alt="Screenshot 2024-06-18 at 11 10 22 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/56c14a7c-4a8c-4c88-944b-6a14fdf6b801">
<img width="753" alt="Screenshot 2024-06-18 at 11 11 05 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/52d1b0cd-31b7-427a-864c-9b89fd31aee0">
<img width="849" alt="Screenshot 2024-06-18 at 11 11 27 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ed3a1d34-d7cc-4094-a8ff-778f77c89d43">
<img width="1120" alt="Screenshot 2024-06-18 at 11 11 37 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/41ed0f8f-61c9-484e-ae3d-0f235e85b66d">

Reading and Writing Cookie is a very challenging task. Cookie information might be huge. There's restriction as well on Cookie size.

There are a lot of limitations associated with Cookies.

# Session

Sessions are also a kind of Cookie.

<img width="1137" alt="Screenshot 2024-06-18 at 11 19 40 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/bee440eb-a8cc-4e38-8979-3c0843065ae8">
<img width="1440" alt="Screenshot 2024-06-18 at 11 19 54 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9e8179ca-1c5b-4101-941d-b04289dec395">
<img width="545" alt="Screenshot 2024-06-18 at 11 21 58 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/e13a2844-19ee-4a54-8045-0de6d9e966e6">
<img width="1157" alt="Screenshot 2024-06-18 at 11 23 57 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/aeb49cae-7450-492a-a1a9-5e0350d01eb8">

- Server keeps the user info in Server memory and with that user ID, it generates a Cookie which is sent to the Client.
  Once Response is sent, the connection is dropped.

- When we send another Request to the Server, the Cookie is also sent to the Server. Server then finds the items in storage and sends 
 personalized Response.

- The difference is, this time, info is not written onto the Cookie but just the user ID which is specific to a particular user. Related 
  info is stored in Server storage.

- Size limit is a major issue with Cookies which is not the case with Session.

- Creating and retrieving Cookie is also cumbersome.

## Captures UserName and pre-populates it next time onwards (using Session)

*"request.getSession"* takes care of creating and managing Cookies behind the scene. If it's a new user, creates a new Session but if it already exists then retrives the same.

<img width="1045" alt="Screenshot 2024-06-18 at 11 39 32 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/34a5662c-4fab-41e1-85df-e0003184cf36">
<img width="992" alt="Screenshot 2024-06-18 at 11 43 07 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/82cc8fae-f279-497c-91dc-4d506a370f30">

We can use the same anywhere now

<img width="981" alt="Screenshot 2024-06-18 at 11 46 42 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/eefab3fa-e79d-4a76-b8b9-a28ba538fa62">
<img width="886" alt="Screenshot 2024-06-18 at 11 47 52 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2400201c-c0e3-4525-b7d2-5da023df8539">

Run the Application

<img width="731" alt="Screenshot 2024-06-18 at 11 48 20 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/56431da8-1371-45e5-8022-7f6c97705154">
<img width="670" alt="Screenshot 2024-06-18 at 11 48 29 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a1d2b5b7-7c30-4636-9450-4bb54147d7e7">

Pre-populates name now

<img width="661" alt="Screenshot 2024-06-18 at 11 48 35 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/1c64a139-0fe0-41b3-a47a-88d3001a454e">
<img width="643" alt="Screenshot 2024-06-18 at 11 48 58 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d33ee88f-11c6-4eb2-a443-a80c52e4e4cf">

This attribute is available to all the Controllers and jsp pages.

In Controllers, we can get the attribute using *"session.getAttribute(\<attribute-name\>)"*

<img width="1026" alt="Screenshot 2024-06-18 at 11 53 28 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/768c767f-1360-46f3-a91b-dbe299ca1ebf">

We can use HttpSession directly as well,

<img width="774" alt="Screenshot 2024-06-19 at 7 00 03 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/0eb2b2a7-8429-4a2d-b3c1-ff456c58b586">

## Note
Session uses Cookie behind the scene.

When we initially visit the website, we can see a Cookie gets created. The Cookie has a JSESSIONID whi has a value associated. The value is nothing but the ID that the Server uses to keep track of the User.

<img width="774" alt="Screenshot 2024-06-18 at 11 57 48 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/74488072-6a8f-4138-aa18-361c8631ae07">

When we login or do others stuffs, since Server accesses the Jsp pages for the first time, behind the scene, it creates a Cookie for the User with JSESSIONID. We can disable this feature as well. All required info is stored in the Server memory and the key is used to track the user for future personalized results.

*FYI:*

<img width="925" alt="Screenshot 2024-06-19 at 7 00 54 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/0bb2e615-6351-4c09-848f-c37343f9a4df">
<img width="774" alt="Screenshot 2024-06-19 at 7 00 03 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/0eb2b2a7-8429-4a2d-b3c1-ff456c58b586">




