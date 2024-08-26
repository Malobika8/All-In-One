# Kafka CLI (Open source apache kafka)
 
<img width="1124" alt="Screenshot 2024-08-26 at 9 40 07 PM" src="https://github.com/user-attachments/assets/340b5971-b9b5-436d-8de2-6fac5cc989c7">

Default port:

<img width="728" alt="Screenshot 2024-08-26 at 10 08 46 PM" src="https://github.com/user-attachments/assets/a79ffa57-ada5-4f40-9ab8-3ecf4875a762">

1. Start ZooKeeper: Open a terminal in the Kafka folder. We need to read the zookeeper properties file present inside the config folder & run the zookeeper-server-start shell script present
   inside the bin folder. The default port it runs on is 2181.

   <img width="438" alt="Screenshot 2024-08-26 at 9 43 20 PM" src="https://github.com/user-attachments/assets/94a13299-605f-4de9-b0d6-5a0e897dd61e">

2. Start the Kafka server: Open another terminal. We need to run "kafka-server-start.sh" file present in the bin folder & read "server.properties" file present in the config folder. The default
   port it runs on is 9092.

   <img width="439" alt="Screenshot 2024-08-26 at 10 07 04 PM" src="https://github.com/user-attachments/assets/a10785cd-d00a-4ae0-844e-d6f2a1bc920e">

3. Create a Topic & specify partition & replication factor.

   In the bin folder, there's a "kafka-topic.sh" file that needs to  be run. We need to also provide host & port of bootstrap/kafka server. We can mention it as "--bootstrap-server localhost:9092".
   We need to provide action and topic name ("--create --topic \<topic-name>. We can define partition as well ("--partition \<n>"). If we don't mention anything, the partition will be
   considered as 1 by default. We need to provide a replication factor ("--replication-factor 1") as well. Since currently only the broker is up and running, we can mention it as 1.

   <img width="960" alt="Screenshot 2024-08-26 at 10 19 04 PM" src="https://github.com/user-attachments/assets/645e22f2-3271-4f4c-91ea-cbcb9cd781af">
   <img width="1114" alt="Screenshot 2024-08-26 at 10 19 41 PM" src="https://github.com/user-attachments/assets/fb6799a1-f5f7-4ea6-a49a-f20253a3c743">

   We can define "n" number of topics.

   To list down, we can run

   <img width="1056" alt="Screenshot 2024-08-26 at 10 20 33 PM" src="https://github.com/user-attachments/assets/d705a0c5-a3ef-4c04-b833-af535068bb88">

   If we want the description of the topic, we can run

   <img width="1112" alt="Screenshot 2024-08-26 at 10 22 20 PM" src="https://github.com/user-attachments/assets/4512b46a-bb2d-49b8-8f36-edda12d618fe">

4. Push messages from the producer to the broker and check if the consumer receives the same. We can monitor everything with Offset Explorer. We need to create a connection (provide the name of the
   cluster, host & port of ZooKeeper).

   <img width="1139" alt="Screenshot 2024-08-26 at 10 31 09 PM" src="https://github.com/user-attachments/assets/75c2811d-63f5-422e-b5f3-7e599f75da47">
   <img width="646" alt="Screenshot 2024-08-26 at 10 32 18 PM" src="https://github.com/user-attachments/assets/c640ba28-768f-4be4-894b-f6f39b5e4815">
   <img width="1144" alt="Screenshot 2024-08-26 at 10 32 30 PM" src="https://github.com/user-attachments/assets/5ec8051c-2cc8-4a12-b4b2-46ff2098f448">
   <img width="1143" alt="Screenshot 2024-08-26 at 10 33 05 PM" src="https://github.com/user-attachments/assets/61f6201d-69c8-4657-bfe7-f8ebd3253268">

   To start the Producer, we can run "kafka-console-producer.sh" present in bin (this is provided by kafka binary). We need to also provide the list of Kafka servers running. We need to
   also provide the topic to which messages are to be pushed.

   <img width="708" alt="Screenshot 2024-08-26 at 10 34 42 PM" src="https://github.com/user-attachments/assets/009300aa-ee95-4592-b117-9a18b9b9269a">
   <img width="999" alt="Screenshot 2024-08-26 at 10 37 34 PM" src="https://github.com/user-attachments/assets/32abf25a-419d-4ea8-9c9d-2bf2253e019a">

   We can now push any messages we want. But before that, we can start the consumer as well so that we can verify that the messages are consumed properly based on the topic.
   Open a new terminal & start consumer.

   <img width="534" alt="Screenshot 2024-08-26 at 10 40 47 PM" src="https://github.com/user-attachments/assets/700a7937-e127-4567-b1da-0b9f9970cffb">

   Push a message from the Producer & it should be visible in the consumer console.

   <img width="1075" alt="Screenshot 2024-08-26 at 10 42 02 PM" src="https://github.com/user-attachments/assets/a03601db-aa15-4d54-aab2-80ef09dc578a">
   <img width="1065" alt="Screenshot 2024-08-26 at 10 42 07 PM" src="https://github.com/user-attachments/assets/e9fe484a-ddc1-40d7-b62f-680c30b8875c">

   We can see all the details in Offset Explorer.

   <img width="1141" alt="Screenshot 2024-08-26 at 10 43 06 PM" src="https://github.com/user-attachments/assets/d8e856a0-16f0-416b-936e-eb03ee71c46c">

   We can notice that although we have 3 partitions, all the messages went to partition 1. This cannot be controlled.

   <img width="1147" alt="Screenshot 2024-08-26 at 10 45 23 PM" src="https://github.com/user-attachments/assets/ce7d515c-adc7-4f95-a521-7a81c62983ab">

   We can send bulk data(CSV data) & see if messages are logged in different partitions or not. We have a user.csv file whose data we can try to send.

   <img width="593" alt="Screenshot 2024-08-26 at 10 48 07 PM" src="https://github.com/user-attachments/assets/3f0a2cc9-402e-4bf1-a910-aaf3cf496904">

   We can mention the path of the file & data will be published from CSV to the broker.

   <img width="564" alt="Screenshot 2024-08-26 at 10 49 42 PM" src="https://github.com/user-attachments/assets/a7bc18f1-101c-4841-8cb4-22d6150474f1">

   All data can be checked in the consumer console.

   <img width="1175" alt="Screenshot 2024-08-26 at 10 50 59 PM" src="https://github.com/user-attachments/assets/d7f53034-f123-4783-a7cf-001b6ac118e9">

   We can verify the same in Offset Explorer.

   <img width="1140" alt="Screenshot 2024-08-26 at 10 51 26 PM" src="https://github.com/user-attachments/assets/e46ad9d3-f5e3-41d8-9aa5-2e753572f711">

   We can see all the messages again went to Partition 0. However, the behavior is unexpected, and we cannot assume anything. Data can go to any of the partitions available. This is handled
   by coordinator or zookeeper.

   Let's try to send it again. We can see this time some of the messages went to Partition 1 as well.

   <img width="1143" alt="Screenshot 2024-08-26 at 10 53 57 PM" src="https://github.com/user-attachments/assets/6c89a693-dcda-4883-acbd-ec8f66fc6b8a">

# Confluent Kafka

All the steps are the same as before (starting the zookeeper server, Kafka server, producer, consumer, creating topics, etc).

1. Start zookeeper.

   <img width="987" alt="Screenshot 2024-08-26 at 11 02 32 PM" src="https://github.com/user-attachments/assets/d046f97a-382d-47c1-9fee-19482e75f780">

2. Start kafka server.

   <img width="1021" alt="Screenshot 2024-08-26 at 11 02 37 PM" src="https://github.com/user-attachments/assets/faf01e3b-4d21-41d4-9420-fcf28384899b">

3. Create a topic.

   <img width="1110" alt="Screenshot 2024-08-26 at 11 02 42 PM" src="https://github.com/user-attachments/assets/b0288639-56fe-4107-8d28-b04d692abd07">
   <img width="1083" alt="Screenshot 2024-08-26 at 11 03 14 PM" src="https://github.com/user-attachments/assets/e68b037e-6391-4c1a-92ac-c0ae69f1deaf">
   <img width="1078" alt="Screenshot 2024-08-26 at 11 03 20 PM" src="https://github.com/user-attachments/assets/50254d6f-fbc7-4685-938e-9814f6b4b9f3">

4. Start producer and consumer and send/receive messages.

   <img width="654" alt="Screenshot 2024-08-26 at 11 04 24 PM" src="https://github.com/user-attachments/assets/83e993ef-002a-45ab-a286-59961f0897eb">
   <img width="1140" alt="Screenshot 2024-08-26 at 11 14 40 PM" src="https://github.com/user-attachments/assets/5a1d3fc0-63d3-4c32-a4c1-71114c4772c8">
   <img width="1149" alt="Screenshot 2024-08-26 at 11 15 07 PM" src="https://github.com/user-attachments/assets/856fed38-630a-46a4-8ba6-44201a34c988">

   Check in Offset Explorer

   <img width="1149" alt="Screenshot 2024-08-26 at 11 15 34 PM" src="https://github.com/user-attachments/assets/437a1997-1a32-487a-851d-a9449d042353">
   <img width="1131" alt="Screenshot 2024-08-26 at 11 15 47 PM" src="https://github.com/user-attachments/assets/c5eb0425-9fa2-4bc4-b06c-a4469a3743df">

   Read from CSV (send bulk messages).

   <img width="577" alt="Screenshot 2024-08-26 at 11 17 17 PM" src="https://github.com/user-attachments/assets/1ca0366e-67fd-4288-ad7e-5bc27b1debc3">
   <img width="537" alt="Screenshot 2024-08-26 at 11 17 23 PM" src="https://github.com/user-attachments/assets/9835e48b-8321-4ec1-bd56-16dd784c6c37">
   <img width="1130" alt="Screenshot 2024-08-26 at 11 17 50 PM" src="https://github.com/user-attachments/assets/64f49f6e-a824-4c23-91da-2ee93e0d124c">

   This time some messages went to partition 0, some to partition 1 & some to partition 2.

   <img width="845" alt="Screenshot 2024-08-26 at 11 17 58 PM" src="https://github.com/user-attachments/assets/f1dfea52-6d75-4d82-b63b-b0cd9b1221c0">
   <img width="1140" alt="Screenshot 2024-08-26 at 11 18 48 PM" src="https://github.com/user-attachments/assets/348f0c19-d2ef-4013-9ace-2dff31262916">
   <img width="1149" alt="Screenshot 2024-08-26 at 11 19 07 PM" src="https://github.com/user-attachments/assets/59fdf773-928b-417f-9d20-73c9f7c0d7db">
   <img width="1139" alt="Screenshot 2024-08-26 at 11 19 23 PM" src="https://github.com/user-attachments/assets/a4e2fbd0-d86c-4fbe-b01a-baba6c2652fa">

   Everything is the same in Confluent kafka just that some utilities are provided in Confluent.







   
