# Let's try to build Discovery Service Component - Discovery Client
## Steps to create a Discovery Client

How to register our services with the Discovery Server that we created?

1. We need to add a dependency to make our service a client to the Discovery Server that we created.

   <img width="814" alt="Screenshot 2024-07-13 at 10 50 58 AM" src="https://github.com/user-attachments/assets/2f7eaab2-b424-4e66-bef0-3d70a5f155ea">

  ```
   <dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
			<version>4.1.3</version>
		</dependency>
  ```
2. Run the Application.

   <img width="557" alt="Screenshot 2024-07-13 at 11 15 42 AM" src="https://github.com/user-attachments/assets/eaed5bc5-0e97-47cb-b5ef-f8a7bd36a28e">
   <img width="871" alt="Screenshot 2024-07-13 at 11 14 32 AM" src="https://github.com/user-attachments/assets/89e6c51d-a5c4-4639-91b2-73726116c7de">
   <img width="1339" alt="Screenshot 2024-07-13 at 11 13 44 AM" src="https://github.com/user-attachments/assets/dddb4f6b-adae-4ba2-9562-53fe528dd4da">
   <img width="570" alt="Screenshot 2024-07-13 at 11 16 16 AM" src="https://github.com/user-attachments/assets/096168a9-7746-4da5-b81f-2a83a8226833">

   We can see address service in Discovery Server list

   <img width="1400" alt="Screenshot 2024-07-13 at 11 16 41 AM" src="https://github.com/user-attachments/assets/9b30c8a3-d2f7-46d6-9971-ad25e37af429">

   We can click on the service actuator link and try hitting our endpoint to see if it works as expected.

   <img width="962" alt="Screenshot 2024-07-13 at 11 19 15 AM" src="https://github.com/user-attachments/assets/7924698d-5042-491d-85ba-7e15f7c5c2f0">
   <img width="1094" alt="Screenshot 2024-07-13 at 11 17 58 AM" src="https://github.com/user-attachments/assets/939c378e-e76d-4267-9a7e-6764beffc2db">

   We can try running another instance and see if it is reflected in the Discovery Server.

   <img width="988" alt="Screenshot 2024-07-13 at 11 19 47 AM" src="https://github.com/user-attachments/assets/81de0368-b262-4fc8-a47b-fb72f9125e09">
   <img width="1102" alt="Screenshot 2024-07-13 at 11 19 59 AM" src="https://github.com/user-attachments/assets/cf322da7-d8f6-4d9c-b4a8-3f9fa5e97624">
   <img width="1095" alt="Screenshot 2024-07-13 at 11 21 40 AM" src="https://github.com/user-attachments/assets/be51435f-b16e-42c3-a334-7a79fd4c1299">
   <img width="960" alt="Screenshot 2024-07-13 at 11 22 16 AM" src="https://github.com/user-attachments/assets/eac052c5-cc1a-4625-b0df-7303744cd7ce">

   We can do the same for *employee-service*

   <img width="1113" alt="Screenshot 2024-07-13 at 11 23 09 AM" src="https://github.com/user-attachments/assets/9e921fd8-48e5-4a4f-b4f7-968e9bb2d703">
   <img width="1354" alt="Screenshot 2024-07-13 at 11 24 34 AM" src="https://github.com/user-attachments/assets/889713e4-cd07-48ac-804b-96bd43900b20">
   <img width="1439" alt="Screenshot 2024-07-13 at 11 25 03 AM" src="https://github.com/user-attachments/assets/71e1ff6f-a7b7-4a11-a68f-0e54b43232af">
   <img width="1382" alt="Screenshot 2024-07-13 at 11 26 23 AM" src="https://github.com/user-attachments/assets/31e7ffaa-b64d-48bb-be21-89686c971c9f">
   <img width="1134" alt="Screenshot 2024-07-13 at 11 27 59 AM" src="https://github.com/user-attachments/assets/ef1732fd-37eb-4be3-b94a-52f81a7ae034">

# How does Eureka Client connect with Eureka Server?

<img width="1119" alt="Screenshot 2024-07-13 at 11 38 51 AM" src="https://github.com/user-attachments/assets/12df5216-1e13-495c-9aa5-98a261b18a2e">

### What happens when we change the port of Eureka Server?

<img width="1086" alt="Screenshot 2024-07-13 at 11 39 51 AM" src="https://github.com/user-attachments/assets/86180e99-6110-4d73-bf7f-195df5738c46">

Let's change the port number for Discovery Service & run address-service

<img width="827" alt="Screenshot 2024-07-13 at 11 40 49 AM" src="https://github.com/user-attachments/assets/3dddc62d-4df3-4c08-bf2f-66602aab11ea">

No running instances.

<img width="1154" alt="Screenshot 2024-07-13 at 11 43 02 AM" src="https://github.com/user-attachments/assets/84413e53-edcf-409c-95aa-61fd43465ac2">
<img width="1137" alt="Screenshot 2024-07-13 at 11 44 37 AM" src="https://github.com/user-attachments/assets/e52d2987-ce53-485e-b53e-b3307933595f">

In our services (*address-service & emp-service*), we need to mention the port for Discovery Server

<img width="839" alt="Screenshot 2024-07-13 at 11 46 12 AM" src="https://github.com/user-attachments/assets/22cc4db0-04d5-4188-a61a-3951f8b5df16">

If we have zones where Discovery Services are running, we can mention it.

<img width="955" alt="Screenshot 2024-07-13 at 11 48 02 AM" src="https://github.com/user-attachments/assets/e7095ea3-f405-4a75-97f1-f2995faa2ea3">

If there is only one zone, that is going to be our default zone.

<img width="795" alt="Screenshot 2024-07-13 at 11 48 41 AM" src="https://github.com/user-attachments/assets/cbed4046-9278-497a-9cba-cf6fd45813d8">

*service-url* is nothing but a map of zone and value(server URL)

<img width="863" alt="Screenshot 2024-07-13 at 11 49 22 AM" src="https://github.com/user-attachments/assets/9a344181-f8de-4f29-957d-3daeb1527247">
<img width="1151" alt="Screenshot 2024-07-13 at 11 49 58 AM" src="https://github.com/user-attachments/assets/daffb257-fdc4-47df-a8e4-99bda44fe9b6">
<img width="1147" alt="Screenshot 2024-07-13 at 11 50 14 AM" src="https://github.com/user-attachments/assets/6b0b6456-1a0a-41ca-9df0-efb639842915">
<img width="781" alt="Screenshot 2024-07-13 at 11 51 33 AM" src="https://github.com/user-attachments/assets/8bf1761f-e66a-4ee6-b1ef-8580b41d608c">

Run the address-service

<img width="1147" alt="Screenshot 2024-07-13 at 11 52 33 AM" src="https://github.com/user-attachments/assets/8320ea35-9c5e-49de-b806-d33996578662">

## FYI
1. We get this exception because of missing HeartBeat

   <img width="1141" alt="Screenshot 2024-07-13 at 11 53 41 AM" src="https://github.com/user-attachments/assets/62f140cf-cf1b-40a2-86a9-7e37e4b3b25e">

2. We can use @EnableEurekaClient for clients

   <img width="799" alt="Screenshot 2024-07-14 at 2 01 56 PM" src="https://github.com/user-attachments/assets/2ea14d04-f9cf-4fa4-ad35-68dec041c28c">

   But it is not a generic annotation. We can use this instead - *@EnableDiscoveryClient*

   <img width="785" alt="Screenshot 2024-07-14 at 2 03 03 PM" src="https://github.com/user-attachments/assets/5b7868a1-5937-4317-8623-1b5b554623f9">





