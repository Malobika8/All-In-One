# Message Routing with specific partitions in Kafka

## Produce messages to a specific partition
### Typical producer flow

- Create a topic with 5 partition count. 

  <img width="437" alt="Screenshot 2024-08-28 at 1 42 34 PM" src="https://github.com/user-attachments/assets/2e28d661-c6a9-48c6-86eb-ed1b00ac7f47">

- Update Producer & Consumer
- Start Zookeeper & Kafka
- Start Producer & Consumer
- Hit the endpoint

  <img width="798" alt="Screenshot 2024-08-28 at 1 46 20 PM" src="https://github.com/user-attachments/assets/58991e1f-8db0-4383-bb75-19463f619f47">

- Verify

  <img width="1146" alt="Screenshot 2024-08-28 at 1 46 38 PM" src="https://github.com/user-attachments/assets/497731e4-d3ce-47a9-995d-38faa89d284d">

  We can check the number of messages logged in each partition.
  
  <img width="1145" alt="Screenshot 2024-08-28 at 1 46 56 PM" src="https://github.com/user-attachments/assets/5f760e74-04a3-4880-9109-db2d3610026d">
  <img width="1142" alt="Screenshot 2024-08-28 at 1 47 03 PM" src="https://github.com/user-attachments/assets/97f3aacd-f4cc-4ba9-88dd-1b3aa57ecee0">
  <img width="1135" alt="Screenshot 2024-08-28 at 1 47 07 PM" src="https://github.com/user-attachments/assets/f8bf73cb-3c75-4539-b548-1f334deeee2b">
  <img width="1137" alt="Screenshot 2024-08-28 at 1 47 10 PM" src="https://github.com/user-attachments/assets/a4e57bac-db12-45cb-9b15-a7ee8435dc8a">
  <img width="1133" alt="Screenshot 2024-08-28 at 1 47 14 PM" src="https://github.com/user-attachments/assets/5e305db0-29dc-4bfd-9055-8f94693e1103">

### How to control producer flow

We want to control the flow so that all the messages go to a single partition.

Let's see how we can send messages to a single partition (say Partition 3). We would need to tell the Kafka template the partition where the 
messages are to be sent.

In "*KafkaTemplate*" class, "*send*" method is overloaded. We can see there's a method that takes partition as a parameter as well. We can
specify which partition we want our messages to go. Key helps in avoiding duplicate messages in Kafka.

<img width="787" alt="Screenshot 2024-08-28 at 1 51 49 PM" src="https://github.com/user-attachments/assets/8dbe814e-6e40-4c79-8254-1d1e823c4bf8">
<img width="789" alt="Screenshot 2024-08-28 at 1 55 12 PM" src="https://github.com/user-attachments/assets/7e0b225c-ba40-4882-8ff7-2e70cdd4b908">

Rerun & verify (Send 100 messages)

<img width="1055" alt="Screenshot 2024-08-28 at 1 56 38 PM" src="https://github.com/user-attachments/assets/0c9f39c5-50ff-475d-9b56-ef5dfa068a87">

Initially, the count in partition 3 was 709. 

<img width="1145" alt="Screenshot 2024-08-28 at 1 59 46 PM" src="https://github.com/user-attachments/assets/22c87f41-6ff0-43a8-a41d-877532e54f26">
<img width="1144" alt="Screenshot 2024-08-28 at 1 58 41 PM" src="https://github.com/user-attachments/assets/4384133f-564a-43ce-847a-e4fa02db40ac">

## Consume messages from a specific partition

We can specify from which partition the consumer instance should consume the messages.

<img width="1104" alt="Screenshot 2024-08-28 at 2 05 44 PM" src="https://github.com/user-attachments/assets/4ccdbcc2-25a6-4981-97cf-f5a84494ab1a">

From the producer, we can send messages to all different partitions available. However, the consumer instance should consume from partition 2
only.

<img width="1122" alt="Screenshot 2024-08-28 at 2 07 28 PM" src="https://github.com/user-attachments/assets/a68b8d23-f9e0-406f-99c8-2a519ea1ecab">

Rerun and verify.

<img width="1030" alt="Screenshot 2024-08-28 at 2 10 04 PM" src="https://github.com/user-attachments/assets/c8af4713-419c-4760-bdd2-37fea47783c5">
<img width="1144" alt="Screenshot 2024-08-28 at 2 11 15 PM" src="https://github.com/user-attachments/assets/2724ac91-d14d-49ce-9b43-2b05df33d429">

The consumer only consumes the messages from Partition 2.

<img width="1027" alt="Screenshot 2024-08-28 at 2 11 04 PM" src="https://github.com/user-attachments/assets/3a4f17f1-eeba-4e87-a837-e163cbad60ba">






 


 

 

