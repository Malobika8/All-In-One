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

## Start Zookeeper & Kafka and run the producer application

We'll try to send bulk messages. We have 3 partitions. Let's try to see how many messages gets stored in different partitions.

<img width="998" alt="Screenshot 2024-08-28 at 8 15 58 AM" src="https://github.com/user-attachments/assets/6bf91097-2611-468a-83e5-33f06ce45f8c">
<img width="860" alt="Screenshot 2024-08-28 at 8 16 37 AM" src="https://github.com/user-attachments/assets/4a3eafab-c957-4b78-ac03-53c348e4ab20">
<img width="1139" alt="Screenshot 2024-08-28 at 8 17 01 AM" src="https://github.com/user-attachments/assets/2757e6e4-90b7-4732-981a-221d26772d65">
<img width="1139" alt="Screenshot 2024-08-28 at 8 17 24 AM" src="https://github.com/user-attachments/assets/65cc75d0-6001-4d53-a935-aadba7b140d5">
<img width="1130" alt="Screenshot 2024-08-28 at 8 17 33 AM" src="https://github.com/user-attachments/assets/c2148de0-c5fc-4154-905b-5cebda933787">
<img width="1128" alt="Screenshot 2024-08-28 at 8 17 48 AM" src="https://github.com/user-attachments/assets/17793678-a292-4e91-9905-b09a392df2dc">
<img width="1140" alt="Screenshot 2024-08-28 at 8 17 53 AM" src="https://github.com/user-attachments/assets/de2ae186-8d96-4dfa-9b73-6ff2830045b5">

Message load has been distributed to all 3 partitions.

## Topic creation

We can either create a topic from the console directly or we can do it programmatically.

Let's see how it can be configured programmatically.

<img width="1105" alt="Screenshot 2024-08-28 at 8 25 08 AM" src="https://github.com/user-attachments/assets/6a618d1d-3e01-480e-9590-06de079f3b40">
<img width="140" alt="Screenshot 2024-08-28 at 8 25 51 AM" src="https://github.com/user-attachments/assets/e69f922b-53ba-40eb-9fa9-11227ebcbdaf">
<img width="139" alt="Screenshot 2024-08-28 at 8 26 02 AM" src="https://github.com/user-attachments/assets/6a774ca3-0065-4c8e-9285-59f548e27882">
<img width="1144" alt="Screenshot 2024-08-28 at 8 26 44 AM" src="https://github.com/user-attachments/assets/d61d92d2-f72f-48a7-ae2d-6e66ebe4b96b">
