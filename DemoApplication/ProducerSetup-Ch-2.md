## Setup

1. Create a producer project with the required dependencies

   <img width="1295" alt="Screenshot 2024-08-25 at 12 24 51 PM" src="https://github.com/user-attachments/assets/ec0c34fb-d5d7-4051-a63c-4ed959921796">
   
2. Add properties to the *application.properties* file.

   <img width="1036" alt="Screenshot 2024-08-25 at 12 38 08 PM" src="https://github.com/user-attachments/assets/397eae33-a45b-4cda-a269-e9ea4ac7f1e9">

3. Create a config topic

   <img width="1019" alt="Screenshot 2024-08-25 at 12 38 47 PM" src="https://github.com/user-attachments/assets/7494a980-7650-458a-817e-b96ec6e0bf4e">

4. Create a bean for WebClient

   <img width="1026" alt="Screenshot 2024-08-25 at 12 39 30 PM" src="https://github.com/user-attachments/assets/fe7c4b7a-e503-4169-a0b1-a958e8991d83">

5. Create producer

   <img width="1037" alt="Screenshot 2024-08-25 at 12 39 54 PM" src="https://github.com/user-attachments/assets/521c987f-4a70-4bad-80ac-68563b093a54">

6. Create Stream Consumer service (the one that will consume stream API & publish the message to a Kafka topic)

   - Create Stream consumer & configure WebClient object.
   - Create a method to consume coming from the URL & publish it to our Kafka broker.

   <img width="1029" alt="Screenshot 2024-08-25 at 12 51 04 PM" src="https://github.com/user-attachments/assets/f356e922-1216-48e0-ac2e-27cb935d0522">

7. Create a Rest API to trigger stream consumption from Wikimedia.

   <img width="1035" alt="Screenshot 2024-08-25 at 12 54 57 PM" src="https://github.com/user-attachments/assets/8434f380-a92c-44f5-a2fe-5239f63b3298">


## Run the application

It should be able to consume a stream of data from Wikimedia

<img width="862" alt="Screenshot 2024-08-25 at 1 03 08 PM" src="https://github.com/user-attachments/assets/d42b6b9b-1761-4bf9-89f2-9c08adff95d1">
<img width="1350" alt="Screenshot 2024-08-25 at 1 03 28 PM" src="https://github.com/user-attachments/assets/4a097201-1a7e-459d-af68-d1512e198075">
<img width="1338" alt="Screenshot 2024-08-25 at 1 03 35 PM" src="https://github.com/user-attachments/assets/522e8b72-c883-4634-bb2d-bea9ebea9495">

## Enable Producer to publish this data to Kafka topic

Use "*sendMessage()*" method of **WikimediaProducer**.

<img width="1035" alt="Screenshot 2024-08-25 at 1 07 59 PM" src="https://github.com/user-attachments/assets/c3a2abe4-b611-4913-ace3-a78943898670">

Restart the application. Data should be published to our Kafka broker now.











