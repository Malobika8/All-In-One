# Microservices Communication

Objective: emp-service should get us address details as well when we hit the employee endpoint.

<img width="1196" alt="Screenshot 2024-07-11 at 8 18 01 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/43f0daa0-f0bc-4865-84a1-9376eac8cec2">

Set context path

<img width="1042" alt="Screenshot 2024-07-11 at 11 05 20 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9a544b9f-cc0a-41fb-840e-73bc90dac147">

To make rest calls, we can use Rest Template.
From Spring 5 RestTemplate is deprecated and no autoconfiguration is provided. Hence, we need to create a bean for it manually.
