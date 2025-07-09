## How Eureka works internally?

The *@EnableEurekaServer* creates a Bean internally named *Marker*. If we check the annotation, we would find that it imports *EurekaServerAutoConfiguration*.

<img width="613" alt="Screenshot 2024-07-14 at 11 07 53 AM" src="https://github.com/user-attachments/assets/765df292-8fb7-479c-a003-8671f69bbd9f">

*EurekaServerAutoConfiguration* autoconfigures Eureka Server for us. It gets triggered on availability of a bean named *Marker*.

<img width="765" alt="Screenshot 2024-07-14 at 11 05 58 AM" src="https://github.com/user-attachments/assets/c29290aa-a9cd-4952-a8ac-00c40a611a30">
<img width="620" alt="Screenshot 2024-07-14 at 11 06 46 AM" src="https://github.com/user-attachments/assets/517c0967-f99a-40cc-85f4-204dcff84ea5">

## How do we know if our microservice instances register themselves on startup?

We can check logs and confirm the same.

<img width="953" alt="Screenshot 2024-07-14 at 11 19 49 AM" src="https://github.com/user-attachments/assets/43f43e10-bd69-4a10-af7c-2b506362261c">

It basically hits the Eureka Server rest endpoint which has all the registry details,

<img width="1090" alt="Screenshot 2024-07-14 at 11 22 50 AM" src="https://github.com/user-attachments/assets/9a3be05a-b2c5-41b8-9455-d3715786e437">

The clients send Heartbeat in 30secs(default)(changeable) for the server to know that they are alive. Also, they look for any updates in the registry and caches the same.

Note: First time it hits "eureka/apps" and gets all the registry details. Next time onwards, it hits "eureka/apps/delta" and gets just the registry changes/updates.

<img width="950" alt="Screenshot 2024-07-14 at 11 24 41 AM" src="https://github.com/user-attachments/assets/42c0c9a5-215d-4219-873e-16c7c67d8b24">
<img width="932" alt="Screenshot 2024-07-14 at 11 25 52 AM" src="https://github.com/user-attachments/assets/eb7e6555-9873-424a-82bf-6c4b81f3fd87">
<img width="727" alt="Screenshot 2024-07-14 at 11 26 59 AM" src="https://github.com/user-attachments/assets/7c38e1e0-407b-4c3e-a70c-0c781fcd5a33">
<img width="682" alt="Screenshot 2024-07-14 at 11 48 17 AM" src="https://github.com/user-attachments/assets/1628778a-94da-4b6a-860f-86cc88dcf802">

We can see, in every 30secs, discovery service logs the same.

<img width="860" alt="Screenshot 2024-07-14 at 11 27 48 AM" src="https://github.com/user-attachments/assets/b16c88a5-5697-4f39-aba1-18a60cc58120">

When the service instance is removed, we get another log message

<img width="779" alt="Screenshot 2024-07-14 at 11 29 52 AM" src="https://github.com/user-attachments/assets/4199ebc4-fa57-4453-93f4-bc46481dd3ec">

### We can see all the endpoints that our MicroServices hits for different tasks.

### https://github.com/Netflix/eureka/wiki/Eureka-REST-operations

### Note:
*The service doesn't go to Eureka registry instantly whenever we start the service. It immediately shows up in Eureka UI but registry is done once the Discovery Service recives first 
Heartbeat from Eureka Client (our microservices). Similar is the case while removing the service from registry.*

## TCP/IP Monitor

We can track all calls using TCP/IP monitor.

<img width="1087" alt="Screenshot 2024-07-14 at 12 05 17 PM" src="https://github.com/user-attachments/assets/84e159d3-79a5-46f1-ba06-4e4ed318926a">
<img width="852" alt="Screenshot 2024-07-14 at 12 10 40 PM" src="https://github.com/user-attachments/assets/f2a6b6b2-dfc3-4b52-b58d-3b8c344117e7">
<img width="608" alt="Screenshot 2024-07-14 at 12 12 13 PM" src="https://github.com/user-attachments/assets/a9fd88f4-4a1f-4afc-9b78-2dcdee3bbc3e">

Start and monitor and we'll be able to track all the calls.

<img width="1117" alt="Screenshot 2024-07-14 at 12 13 20 PM" src="https://github.com/user-attachments/assets/c0c3b6ae-b822-41a6-b6c4-00a0d716be6f">
<img width="890" alt="Screenshot 2024-07-14 at 12 14 20 PM" src="https://github.com/user-attachments/assets/f7cc835a-f395-4b29-8202-694626527755">
<img width="578" alt="Screenshot 2024-07-14 at 12 14 36 PM" src="https://github.com/user-attachments/assets/f7a2d60e-3f9b-43e8-abd7-1eb4a0782dd1">

- The first call is empty since there's no instance registered with the DiscoveryService

  <img width="903" alt="Screenshot 2024-07-14 at 12 16 16 PM" src="https://github.com/user-attachments/assets/6f916c92-d52f-45d8-b824-cfc8c9bac36b">

- Then, it makes a POST call and registers itself

  <img width="887" alt="Screenshot 2024-07-14 at 12 17 11 PM" src="https://github.com/user-attachments/assets/8fbe24e3-9871-4bd3-9bab-42596a843d92">

- After 30 seconds, we can see the instance registered and hence listed in the Registry list.

  <img width="890" alt="Screenshot 2024-07-14 at 12 19 04 PM" src="https://github.com/user-attachments/assets/8dc5bd45-3a48-424d-bcb1-4f7b3f83051f">

- Next up, it sends a HeartBeat

  <img width="881" alt="Screenshot 2024-07-14 at 12 20 11 PM" src="https://github.com/user-attachments/assets/394f8d51-ea4b-466f-a8d4-a66cc2d718a0">

- Next time onwards, it keeps on checking for updates through *delta* endpoint.

  <img width="891" alt="Screenshot 2024-07-14 at 12 21 33 PM" src="https://github.com/user-attachments/assets/f3203aaf-f011-47a4-84bb-4a94cff42fb6">


### Q. Why do we turn off the fetch registry from the Server side?



