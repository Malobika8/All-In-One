# Send data in JSON format

There are a lot of built-in serializers & deserializers but there aren't any for JSON. The reason why Apache doesn't provide one is to avoid imposing a specific serialization format on users.
So, Kafka is designed to be agnostic to the data formats to be used by producers & consumers allowing flexibility in accommodating various data structures & serialization formats.
However, Spring Kafka created a JSON serializer & deserializer which can be used to convert Java objects to & from JSON.

Let's see how we can send Java objects in JSON format from the producer & consume the same in JSON.

- We need to first edit the configuration/properties.

  <img width="1028" alt="Screenshot 2024-08-25 at 10 49 55 AM" src="https://github.com/user-attachments/assets/42ab5a5a-6ef9-4c51-8296-41d88ab5d928">

- Create an object that we want to send from the producer & consume by the consumer

  <img width="914" alt="Screenshot 2024-08-25 at 10 57 43 AM" src="https://github.com/user-attachments/assets/c47aeca0-14e9-4c4b-9883-cd46c82cbd20">

- Create Producer: We need to create a message first and then we can make use of the *sendMessage()* method in **KafkaTemplate** that takes **Message** as a parameter.

  <img width="1022" alt="Screenshot 2024-08-25 at 10 59 29 AM" src="https://github.com/user-attachments/assets/b046b4fb-02e6-4a9c-839a-de5ddae44267">

- Update MessageController

  <img width="1020" alt="Screenshot 2024-08-25 at 11 01 42 AM" src="https://github.com/user-attachments/assets/40cb5c94-1d49-4990-9882-8a2c0c57be28">

  Note that it is better to avoid having two producers injected which more or less does the same thing. This is currently done for understanding purposes.

- Update Consumer: Note that our Consumer has String in it although we are using JsonDeserializer.

  When we run the application, we might get an error that the package is not trusted.

  <img width="1343" alt="Screenshot 2024-08-25 at 11 37 38 AM" src="https://github.com/user-attachments/assets/41477769-853f-4560-a7b1-607de06dd824">

  To enable trusted packages,

  <img width="792" alt="Screenshot 2024-08-25 at 11 11 55 AM" src="https://github.com/user-attachments/assets/c2e89b88-ca0c-48f3-bdc4-40a9a3784513">
  <img width="1022" alt="Screenshot 2024-08-25 at 11 58 54 AM" src="https://github.com/user-attachments/assets/1cea303b-0ac0-44e9-9878-aaa45a19a151">

  When we try to run now, we will come across another error - "Student cannot be converted to String".

  <img width="1347" alt="Screenshot 2024-08-25 at 11 44 03 AM" src="https://github.com/user-attachments/assets/d76fedfb-a74b-4c40-badd-9457916195a5">
  <img width="1276" alt="Screenshot 2024-08-25 at 11 44 10 AM" src="https://github.com/user-attachments/assets/45e5ef25-a0b5-4ff4-932c-00e371c6ad5f">

  In that case, we would need to add KafkaJsonConsumer.

  <img width="1028" alt="Screenshot 2024-08-25 at 11 45 19 AM" src="https://github.com/user-attachments/assets/de062cb6-3c97-4774-a0cb-f47c0477fdba">

  Make sure to comment out the old Listener.

  <img width="1024" alt="Screenshot 2024-08-25 at 11 45 01 AM" src="https://github.com/user-attachments/assets/df6393f8-37f5-4df4-952c-106bb72d42a8">

- Run the application & it should work as expected.

  <img width="1342" alt="Screenshot 2024-08-25 at 11 46 55 AM" src="https://github.com/user-attachments/assets/b62f30a9-4e9c-4b56-b912-c2d03b94f3ed">
  <img width="1032" alt="Screenshot 2024-08-25 at 11 47 05 AM" src="https://github.com/user-attachments/assets/a7aeb6f9-f86f-487f-bdfe-9f7d489bfa23">
  <img width="1329" alt="Screenshot 2024-08-25 at 11 47 16 AM" src="https://github.com/user-attachments/assets/57158d38-db2a-4ef7-8635-d1938bcab0ce">

  We can call *toString()* for object details to be logged. (Note that *toString()* should be implemented in Student for this to work)

  <img width="1024" alt="Screenshot 2024-08-25 at 11 54 15 AM" src="https://github.com/user-attachments/assets/76534bb6-d5af-4c40-a765-a49a7a8f4cb5">
  <img width="1044" alt="Screenshot 2024-08-25 at 11 54 30 AM" src="https://github.com/user-attachments/assets/fa25bcd9-f541-4468-8ec1-1541f10a5630">
  <img width="1335" alt="Screenshot 2024-08-25 at 11 56 49 AM" src="https://github.com/user-attachments/assets/58070712-68ca-4819-8f2c-3ebdc62c6738">


  



