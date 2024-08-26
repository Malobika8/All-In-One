# Architecture & Components

<img width="1071" alt="Screenshot 2024-08-26 at 11 42 51 AM" src="https://github.com/user-attachments/assets/9d4281cf-358b-4a69-856d-10463602a2e1">

## Producer | Consumer | Broker | Cluster

A producer is the source of data that publishes the messages/events. However, it doesn't directly communicate with consumers. Broker processes the messages from producer to consumer.
Kafka Broker is nothing but a server. It is just an intermediate entity that helps in message exchange between producer & consumer.

<img width="1011" alt="Screenshot 2024-08-26 at 11 52 01 AM" src="https://github.com/user-attachments/assets/afbb1c7f-7b2b-4128-b974-213dc01d3530">

A cluster is a common terminology in distributed computing systems. It is nothing but a group of computers/servers that work for a common purpose. Kafka is also a distributed system.

<img width="1096" alt="Screenshot 2024-08-26 at 11 53 21 AM" src="https://github.com/user-attachments/assets/614ce314-8ae0-4b31-81b0-b9aec823ef2e">

If producers produce a high volume of data, then a single Kafka broker may be unable to handle the load. In that case, additional Kafka servers/brokers might be needed. We can group multiple 
Kafka borkers in a Kafka cluster.

## Topic

Let's consider the same Paytm example. Broker receives different kinds of messages. It can be a payment transaction, ticket booking, recharge, etc. 

However, how would the consumer determine which one it needs?

<img width="1128" alt="Screenshot 2024-08-26 at 11 59 35 AM" src="https://github.com/user-attachments/assets/469d54d0-ab9d-48c3-8452-584e694227ec">
<img width="1123" alt="Screenshot 2024-08-26 at 12 01 53 PM" src="https://github.com/user-attachments/assets/22ff3ea9-ad2c-4320-a8ab-70a7594b0ad2">

There can be all different types of payment messages. This is when "Topic" comes into the picture. Topic categorizes various types of messages. Different event types can be segregated to 
different topics. 

<img width="1119" alt="Screenshot 2024-08-26 at 12 03 19 PM" src="https://github.com/user-attachments/assets/a364e02b-791f-429c-af37-999b62a4cee5">

Consumers can simply subscribe to the specific topic & get all events/messages related to the same.

It is similar to Database.

<img width="1125" alt="Screenshot 2024-08-26 at 12 07 35 PM" src="https://github.com/user-attachments/assets/72f76227-ede6-4fb4-9e80-b0d9fe807c60">
<img width="671" alt="Screenshot 2024-08-26 at 12 07 53 PM" src="https://github.com/user-attachments/assets/bec6969f-3a22-425e-a6d3-2fe3716670da">

## Partitions

Suppose the producer publishes a huge volume of data. In that case, the topic might not be able to handle those many messages. There could be storage challenges. It can be very challenging 
for the topic to store data on a single machine. Since Kafka is a distributed system, Kafka topics are broken into multiple parts that are distributed into multiple machines. This is
called topic partitioning & each part is called a "*partition*" in Kafka. This gives us better performance & high availability.

<img width="1069" alt="Screenshot 2024-08-26 at 12 14 01 PM" src="https://github.com/user-attachments/assets/e4231c0c-bbab-41ab-8d7f-579a0718a139">

Even if any partition goes down, others will be able to handle the load.

<img width="738" alt="Screenshot 2024-08-26 at 12 17 38 PM" src="https://github.com/user-attachments/assets/7abc4a99-ce93-4d29-8fd0-144e7c6b331c">

Topic partitioning is a key aspect of Kafka & we can decide the number of partitions during topic creation.

## Offset

A Kafka cluster can have one or more Kafka servers/brokers. A Kafka broker can have one or more topics. A Kafka topic can have one or more partitions.

As soon as a message goes to the portion, a number is assigned to the message. This is called "Offset". It's a sequence number assigned to each message.

<img width="1064" alt="Screenshot 2024-08-26 at 12 19 20 PM" src="https://github.com/user-attachments/assets/807de8b8-d580-4d77-95e0-1ac885ca8cca">

The purpose of offset is to keep track of which message is already consumed by the consumer.

<img width="791" alt="Screenshot 2024-08-26 at 12 21 13 PM" src="https://github.com/user-attachments/assets/156aca24-bfd9-488a-baa8-daa802cb6af8">

Consider a scenario where after reading 4 messages, the consumer goes down. 

<img width="1093" alt="Screenshot 2024-08-26 at 12 22 04 PM" src="https://github.com/user-attachments/assets/a2a9440c-e3b9-4a0d-983f-5888d62a16b3">

When the consumer comes back online, then the offset value helps in determining where to start consuming the messages from. 

<img width="1090" alt="Screenshot 2024-08-26 at 12 23 19 PM" src="https://github.com/user-attachments/assets/f504f238-5e63-4374-835f-e33c72f9c8fd">

## Consumer Group

<img width="761" alt="Screenshot 2024-08-26 at 12 32 31 PM" src="https://github.com/user-attachments/assets/d73777d4-5426-4bca-ad9c-f26185ea74fb">

It divides the workload and increases throughput. Consumer instances can also read parallely from different partitions.

<img width="1108" alt="Screenshot 2024-08-26 at 12 27 00 PM" src="https://github.com/user-attachments/assets/f35d770e-3492-4c7a-88d9-6090beea9cb5">

### Disadvantage: Consumer-Partition order is not guaranteed. Any consumer can talk to any partition.

Note that if there's an extra consumer instance, it will sit idle since all other consumers are occupied with all partitions available. If any instance goes down, then the extra one might
get a chance to communicate with a partition. This is called "Consumer Rebalancing".

<img width="1094" alt="Screenshot 2024-08-26 at 12 29 57 PM" src="https://github.com/user-attachments/assets/b61db155-29e5-4ea7-b8be-7dcea39f4cae">

## ZooKeeper

<img width="726" alt="Screenshot 2024-08-26 at 12 33 12 PM" src="https://github.com/user-attachments/assets/0501d34b-3eae-4ea4-a65d-f634bfb42e57">

ZooKeeper acts as a manager for Kafka clusters.

<img width="1102" alt="Screenshot 2024-08-26 at 12 33 31 PM" src="https://github.com/user-attachments/assets/56b23472-2795-4a7f-ad50-a77f3b416273">













