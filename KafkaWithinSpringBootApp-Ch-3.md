# Kafka within Spring Boot Application

- Create the SpringBoot project with required dependencies.

  <img width="1361" alt="Screenshot 2024-08-24 at 9 15 46 PM" src="https://github.com/user-attachments/assets/e98c6c08-d4e7-4389-85cc-7f30ead786ff">

- Configure the Kafka server.

  * ### Consumer Configuration:
    
    Go to application.yml and add properties

    <img width="1025" alt="Screenshot 2024-08-24 at 9 32 04 PM" src="https://github.com/user-attachments/assets/64444ddd-a590-4d89-a3c3-221eea8cc986">

    To create consumer group,

    <img width="904" alt="Screenshot 2024-08-24 at 9 26 07 PM" src="https://github.com/user-attachments/assets/1dc232ec-34d2-4443-b509-665238b48cb7">

    To tell spring what we need to do when we want to use the offset or when we want to reset the offset,

    <img width="1016" alt="Screenshot 2024-08-24 at 9 27 47 PM" src="https://github.com/user-attachments/assets/8dd234ad-776b-4b46-af98-59ba47d3e45f">
    <img width="956" alt="Screenshot 2024-08-24 at 9 27 54 PM" src="https://github.com/user-attachments/assets/f163efbe-a1bb-4d6a-9e34-c086ac5796b6">

    Note that message are serialized in the producer part & deserialized in the consumer part.

    In order to consume a message(we'll consider sending & consuming Strings for now), 

    <img width="956" alt="Screenshot 2024-08-24 at 9 31 09 PM" src="https://github.com/user-attachments/assets/81e96540-7584-4a35-abf4-66d05c580580">

  * ### Producer Configuration:
 
    For this project, we will be producer & consumer at the same time.

    Note that the serializer & deserializer should be of the same type.

    <img width="1004" alt="Screenshot 2024-08-24 at 9 39 01 PM" src="https://github.com/user-attachments/assets/9f883a09-3274-47d0-8c09-690204d33aea">

- Create a new topic

  <img width="1028" alt="Screenshot 2024-08-24 at 9 42 00 PM" src="https://github.com/user-attachments/assets/5b2a6759-bb34-4bac-9bd9-fc5f8bd56883">

- Create a Kafka Producer class:

  KafkaTemplate takes key & value. We have StringSerializer added in properties file. Hence, key & value will be of type String.

  <img width="1023" alt="Screenshot 2024-08-24 at 9 47 59 PM" src="https://github.com/user-attachments/assets/8e7fb3e6-4a2d-40ae-8937-8a7770346d8f">

- Create a RestController in order to be able to call the Kafka Producer.

  <img width="1027" alt="Screenshot 2024-08-24 at 9 51 43 PM" src="https://github.com/user-attachments/assets/d4cfb54b-724e-4a65-9751-0fa258021251">

----------------------
Let's run the Application & test it out.

<img width="1342" alt="Screenshot 2024-08-24 at 9 52 52 PM" src="https://github.com/user-attachments/assets/4fd8e923-f567-4379-bcf2-7bea146a2de9">

Go to "*kafka_server*" folder and open a terminal.

Run the consumer command with our topic name (*malo*). So far we dont have any messages consumed or queued to our application.

<img width="1368" alt="Screenshot 2024-08-24 at 9 55 56 PM" src="https://github.com/user-attachments/assets/ab4bc480-ef78-455f-8852-74a7e8760325">

Go to postman & hit the endpoint.

<img width="854" alt="Screenshot 2024-08-24 at 9 59 04 PM" src="https://github.com/user-attachments/assets/6c472409-ef7f-4d56-b870-cdf71dba316b">

We can see the message in Kafka consumer console.

<img width="1379" alt="Screenshot 2024-08-24 at 9 59 53 PM" src="https://github.com/user-attachments/assets/ed1cbfb7-1a57-4f0d-8bc3-0baa747f2638">

We can also see logs in Intellij.

<img width="1355" alt="Screenshot 2024-08-24 at 10 00 14 PM" src="https://github.com/user-attachments/assets/2d5599dd-be70-4c44-9cc8-d1e6cb18e579">
----------------------

- Create Consumer: Let's now implement a real consumer for our topic.

  <img width="1022" alt="Screenshot 2024-08-24 at 10 07 50 PM" src="https://github.com/user-attachments/assets/102e73e9-0ad2-493c-977b-c641f3206897">

  Let's see of the consumer is consuming the message.

  Run the application,

  <img width="1342" alt="Screenshot 2024-08-24 at 10 08 32 PM" src="https://github.com/user-attachments/assets/56876cdc-62ab-4993-809e-e38b0a146d58">

  Let's send another message using Postman and check.

  <img width="858" alt="Screenshot 2024-08-24 at 10 10 28 PM" src="https://github.com/user-attachments/assets/693f196d-a2b3-45ce-a53a-6f7cc3629cf7">
  <img width="1309" alt="Screenshot 2024-08-24 at 10 10 42 PM" src="https://github.com/user-attachments/assets/0eed2860-9365-4cea-b6a7-6fabb156ce66">

  This is how we can create a consumer for our Application.
  












    
