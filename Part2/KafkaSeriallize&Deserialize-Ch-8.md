# Kafka Serialize & Deserialize

The PubSub system that we designed so far won't accept any data type. 

Let's observe how it behaves when we send an object in the existing code.

1. Create a DTO class.

   <img width="1019" alt="Screenshot 2024-08-28 at 12 00 39 PM" src="https://github.com/user-attachments/assets/953d3713-e74a-4db1-a4a8-7560b94d6059">

2. Update Producer to send object rather than String.

   <img width="735" alt="Screenshot 2024-08-28 at 12 04 34 PM" src="https://github.com/user-attachments/assets/d6dd2b5d-2e75-4265-9ac6-11db327d691d">
   <img width="1105" alt="Screenshot 2024-08-28 at 12 01 34 PM" src="https://github.com/user-attachments/assets/02d252ae-c3ab-493e-a59c-f674439fa3f4">
   <img width="753" alt="Screenshot 2024-08-28 at 12 05 06 PM" src="https://github.com/user-attachments/assets/01e28e08-9c60-4080-869d-327048c321b7">
   <img width="1100" alt="Screenshot 2024-08-28 at 12 03 43 PM" src="https://github.com/user-attachments/assets/1a2b7737-86cc-4b6b-b22d-06b42b9af85d">

   Add try catch to see errors.

   <img width="1038" alt="Screenshot 2024-08-28 at 12 16 17 PM" src="https://github.com/user-attachments/assets/2fa79322-60ef-4339-b487-a59b020b6f0c">

4. Update Consumer to accept Object rather than String.

   <img width="1104" alt="Screenshot 2024-08-28 at 12 11 22 PM" src="https://github.com/user-attachments/assets/28897c75-2f85-4a86-a68d-90320987e719">

5. Start Zookeeper & Kafka server
6. Start Producer
7. Start Consumer

   <img width="1045" alt="Screenshot 2024-08-28 at 12 13 49 PM" src="https://github.com/user-attachments/assets/a5e0f2f8-23c5-41f5-90be-f72f759d0ff6">

8. Hit the endpoint

   <img width="792" alt="Screenshot 2024-08-28 at 12 14 40 PM" src="https://github.com/user-attachments/assets/5cb10a37-cd95-478d-ba8f-d830cd204436">

   We'll come across an error.

   <img width="1109" alt="Screenshot 2024-08-28 at 12 14 57 PM" src="https://github.com/user-attachments/assets/1f033f6a-1244-47e5-8c91-7d7ce61ce5e4">

   Usually, when we send any message to the topic, it sends a byte array as input as we serialize the object.

   <img width="1121" alt="Screenshot 2024-08-28 at 12 18 35 PM" src="https://github.com/user-attachments/assets/340e2e8b-ec53-4a79-aacb-ac08761c3bb4">

   We can happily play with String without adding any configuration. But for different types of objects, we need to mention the serializer
   & deserializer to be used.

   (Update in both Producer & Consumer's application.yml file)
   <img width="1091" alt="Screenshot 2024-08-28 at 12 23 04 PM" src="https://github.com/user-attachments/assets/94953e76-8d90-4dac-9b93-dc57688c6e92">

   We need to specify that we're sending the key as a String for which StringSerializer can be used. However, for value, we're sending an object
   for which JsonSerializer needs to be used.

   <img width="1030" alt="Screenshot 2024-08-28 at 12 26 11 PM" src="https://github.com/user-attachments/assets/76d6d8ea-8fe0-410d-9197-84e2cc8db4ae">

   Rerun Producer & Consumer & hit the endpoint.

   <img width="781" alt="Screenshot 2024-08-28 at 12 27 26 PM" src="https://github.com/user-attachments/assets/d5153dfb-f1f6-4190-8901-a0274924d637">

   No error in Producer & successfully published the message.

   <img width="1090" alt="Screenshot 2024-08-28 at 12 27 32 PM" src="https://github.com/user-attachments/assets/afd59b84-e39e-4ad6-91ad-3c2943e82323">

   Error in Consumer. We need to add the "dto" package to the trusted package list.

   <img width="1047" alt="Screenshot 2024-08-28 at 12 27 45 PM" src="https://github.com/user-attachments/assets/c2f62c8e-6f12-48c9-8291-79639a0927e6">
   <img width="1048" alt="Screenshot 2024-08-28 at 12 31 15 PM" src="https://github.com/user-attachments/assets/02a4b1ce-ef3d-4146-b2d2-46739b36c7c6">

   Rerun consumer.

   <img width="1078" alt="Screenshot 2024-08-28 at 12 31 37 PM" src="https://github.com/user-attachments/assets/f140b142-9715-445d-9481-6ecc1b592512">
   <img width="1036" alt="Screenshot 2024-08-28 at 12 31 42 PM" src="https://github.com/user-attachments/assets/634da061-5019-42ab-9566-8d8dcea1a145">

## Note:

We can do configurations with Java-based configuration classes as well.

Instead of adding properties in the "application.yml" file, we can have a config class to do the same configurations.

### Producer

So, instead of this, 

<img width="1422" alt="Screenshot 2024-08-28 at 12 40 42 PM" src="https://github.com/user-attachments/assets/d6f32206-c316-4165-b2b7-8f8406177aa7">

we can do this,

<img width="1406" alt="Screenshot 2024-08-28 at 12 40 48 PM" src="https://github.com/user-attachments/assets/606f6b58-bae3-4a44-8718-4a3539fa0fda">

### Consumer

<img width="1103" alt="Screenshot 2024-08-28 at 12 43 28 PM" src="https://github.com/user-attachments/assets/ab9d2f05-86af-488f-9a50-2b0e23123d39">
<img width="1038" alt="Screenshot 2024-08-28 at 12 44 24 PM" src="https://github.com/user-attachments/assets/8ac992ee-93cc-4932-a855-2d7dbc6d8e93">
