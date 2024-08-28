# Consumer Example

We need a consumer that can consume events from topics. 

<img width="1070" alt="Screenshot 2024-08-28 at 8 28 42 AM" src="https://github.com/user-attachments/assets/0119071c-5ba3-46b9-a93e-7e074ad90efd">

It should be noted that one consumer consuming from a number of partitions is not a good design. It's better to distribute the workload by having
multiple consumer instances.

<img width="1097" alt="Screenshot 2024-08-28 at 8 30 25 AM" src="https://github.com/user-attachments/assets/bf4b984e-5180-4067-94db-697d4590e359">

Each partition can be consumed by individual consumer instances. It will definitely increase the throughput.

What if we have another consumer instance?

<img width="1103" alt="Screenshot 2024-08-28 at 8 31 31 AM" src="https://github.com/user-attachments/assets/7a434c60-fc7b-4f5c-b051-84c72e140d75">

It will sit idle. If any consumer dies, then the other one will become active. This is called "Consumer Rebalancing".

1. Create a consumer project with the required dependencies

   <img width="1296" alt="Screenshot 2024-08-28 at 8 33 44 AM" src="https://github.com/user-attachments/assets/98a10622-2d87-433e-93e1-fc3dced3d69c">

2. We need to tell the consumer application where our Kafka server is running. Then only it will know where to connect.

   <img width="1395" alt="Screenshot 2024-08-28 at 8 43 15 AM" src="https://github.com/user-attachments/assets/562ae39a-66c3-4698-b6cd-b55912bdd217">

3. Create a Listener that will listen to the topic we created earlier in the Producer project.

   <img width="1417" alt="Screenshot 2024-08-28 at 8 43 26 AM" src="https://github.com/user-attachments/assets/377f7800-d584-4de6-9be2-3ca58b6b526e">

## Run & test

While running the consumer application, we might come across an error.

<img width="1030" alt="Screenshot 2024-08-28 at 8 46 21 AM" src="https://github.com/user-attachments/assets/4a24a96b-576f-434f-ad95-1e46420b66c7">

Even when there's only one consumer instance, we still need to create a group ID.

<img width="719" alt="Screenshot 2024-08-28 at 8 48 41 AM" src="https://github.com/user-attachments/assets/85aaf191-d146-43b6-821a-63b10831a36d">

We need to configure it in application.yml as well.

<img width="798" alt="Screenshot 2024-08-28 at 8 49 35 AM" src="https://github.com/user-attachments/assets/c3972000-7fb3-487d-ae60-e3e2a2f9dc9d">

- Start the producer application.
- Start the consumer application. We can see the group has been assigned to all the 3 partitions.

  <img width="1010" alt="Screenshot 2024-08-28 at 8 50 30 AM" src="https://github.com/user-attachments/assets/4dfe451b-4c30-4fdd-9f36-22ee08851438">
  <img width="1031" alt="Screenshot 2024-08-28 at 8 50 45 AM" src="https://github.com/user-attachments/assets/6d2f2764-1f0e-4304-b08c-4ee1e4eb2e5e">
  
- Hit the endpoint

  <img width="743" alt="Screenshot 2024-08-28 at 8 52 32 AM" src="https://github.com/user-attachments/assets/75c8890b-69fd-4c6f-905c-bb3577ead9bb">

- Check Offset Explorer

  <img width="1030" alt="Screenshot 2024-08-28 at 8 52 44 AM" src="https://github.com/user-attachments/assets/13de313d-b232-4b20-9972-9ea7cbcf8c29">
  <img width="1147" alt="Screenshot 2024-08-28 at 8 53 22 AM" src="https://github.com/user-attachments/assets/55978030-904a-4ad5-b665-98a0eacc7143">
  <img width="1139" alt="Screenshot 2024-08-28 at 8 53 28 AM" src="https://github.com/user-attachments/assets/c09b8756-dc16-4b9e-b210-e0dd5804150f">
  <img width="1141" alt="Screenshot 2024-08-28 at 8 53 37 AM" src="https://github.com/user-attachments/assets/4d701fdf-2950-465f-83c1-c5e69d3db761">
  <img width="1145" alt="Screenshot 2024-08-28 at 8 53 45 AM" src="https://github.com/user-attachments/assets/8a733ba3-ff19-4aa0-b7a3-7675c193dffe">
  <img width="1148" alt="Screenshot 2024-08-28 at 8 53 49 AM" src="https://github.com/user-attachments/assets/6ac94f56-964b-45c7-a16b-a676d99e34af">

  Check in the consumer group

  <img width="1142" alt="Screenshot 2024-08-28 at 8 54 50 AM" src="https://github.com/user-attachments/assets/5bd69648-48a3-4ceb-88ee-3f18ba0b947d">

## Increase consumer instance

Let's create 4 consumer instances & observe the behavior.

<img width="1014" alt="Screenshot 2024-08-28 at 9 56 38 AM" src="https://github.com/user-attachments/assets/76655f50-6cee-427b-a606-50d9b2b7ddc1">

Start the consumer application

<img width="1019" alt="Screenshot 2024-08-28 at 9 57 07 AM" src="https://github.com/user-attachments/assets/e893af29-3d99-487a-b6f3-ba48ccc9f77c">
<img width="739" alt="Screenshot 2024-08-28 at 9 58 06 AM" src="https://github.com/user-attachments/assets/505b3d4f-77fe-455d-8bd5-dd5913739e7f">

We can see all 3 partitions received the messages.

<img width="1143" alt="Screenshot 2024-08-28 at 9 58 28 AM" src="https://github.com/user-attachments/assets/eda9a8f4-eb1b-4ef6-9f1a-036a7baeb46d">

We can see 3 consumer instances out of 4 received the messages.

<img width="771" alt="Screenshot 2024-08-28 at 9 59 45 AM" src="https://github.com/user-attachments/assets/6657cb5b-224b-4863-a0d9-9be0a015a44d">
<img width="912" alt="Screenshot 2024-08-28 at 9 59 57 AM" src="https://github.com/user-attachments/assets/0ec37b3a-65a5-4ace-ba7a-7703506a9968">
<img width="773" alt="Screenshot 2024-08-28 at 10 00 05 AM" src="https://github.com/user-attachments/assets/49de136a-ff64-46ef-bfe2-bd1e38863b05">
<img width="804" alt="Screenshot 2024-08-28 at 10 00 21 AM" src="https://github.com/user-attachments/assets/b95892db-9f5e-4e7c-b8cf-7229b498736f">

This is because we have 3 partitions and those are assigned to 3 consumer instances. The other one stays idle till any of the consumer goes down
or partition increases by 1.

### Note
- The order is not guaranteed. It can be anything.
- In real-time, we should avoid creating consumer instances this way. We can maintain concurrency & do it in a better way.

## What happens when the Consumer goes down in between?

We can check how it behaves when the Consumer goes down. How many messages do consumer instances receive & how do all those instances resume getting
messages once consumer instances come back alive.

It can be checked by "lag".

- Let's try to send 100000 messages.
- Change the topic and group name.
- Immediately after hitting the endpoint, we will stop the consumer application so that we can observe the behavior.

We can check it in the "lag" section in Offset Explorer.

<img width="823" alt="Screenshot 2024-08-28 at 10 10 06 AM" src="https://github.com/user-attachments/assets/6c8c59c9-5c03-40b5-a798-12704d69c674">
<img width="807" alt="Screenshot 2024-08-28 at 10 10 19 AM" src="https://github.com/user-attachments/assets/048e2aae-b403-4a12-b70c-90534503e716">
<img width="798" alt="Screenshot 2024-08-28 at 10 10 39 AM" src="https://github.com/user-attachments/assets/5c40ace6-4158-4b10-8a2f-04d576d6968c">

Change the topic & group ID in the Consumer application.

<img width="1048" alt="Screenshot 2024-08-28 at 10 11 12 AM" src="https://github.com/user-attachments/assets/1fad16ff-a0a4-45a2-a8df-37d9ae0f8109">

Hit the endpoint & stop the consumer immediately.

<img width="1140" alt="Screenshot 2024-08-28 at 10 11 39 AM" src="https://github.com/user-attachments/assets/73d195c2-d8ab-4869-8f85-1583429f26bf">

We can see lag in Offset Explorer.

<img width="1144" alt="Screenshot 2024-08-28 at 10 12 01 AM" src="https://github.com/user-attachments/assets/8f02f226-9cee-4da3-8a90-b881f65a0045">

- End: Total number of messages in topic
- Offset: Number of messages consumed by the Consumer
- Lag: Number of messages left to be consumed by the Consumer

<img width="1001" alt="Screenshot 2024-08-28 at 11 20 06 AM" src="https://github.com/user-attachments/assets/62725e37-4779-4603-8c1d-e92c11063510">
