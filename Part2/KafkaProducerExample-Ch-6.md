# Kafka Producer Example

1. Create producer project with required dependencies

   <img width="1293" alt="Screenshot 2024-08-27 at 12 59 39 PM" src="https://github.com/user-attachments/assets/9bb1abbe-a96c-45e2-a583-c8fd86e46d3d">

2. Start Zookeeper -> Start Kafka
3. Create a file and specify where the kafka server is running.

   <img width="1195" alt="Screenshot 2024-08-27 at 1 06 39 PM" src="https://github.com/user-attachments/assets/2878d06e-7da3-4b6e-912a-dfc74e6b2594">

4. To publish a message from our application and talk to the kafka server, we need to use "KafkaTemplate".

   <img width="1033" alt="Screenshot 2024-08-27 at 1 20 18 PM" src="https://github.com/user-attachments/assets/5ee20d1d-bbb1-467c-a4b6-072a7998aa03">
   <img width="1024" alt="Screenshot 2024-08-27 at 1 20 35 PM" src="https://github.com/user-attachments/assets/d843d2e8-4329-4c3f-97fe-ae387657d413">

   We haven't created the topic manually. We are using KafkaTemplate to create topic while sending the message.
