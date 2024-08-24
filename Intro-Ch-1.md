# Kafka
Apache Kafka isn't just a tool, it is a powerhouse reshaping how we navigate and manage data streams. 

## Agenda
A continuous stream of data orchestrated by a reactive Spring Boot producer seamlessly delivering messages to a Kafka Broker. Diligent consumer transcribing messages into DynamoDB.

### Message Broker
It's an intermediary software component responsible for facilitating communication & data exchange between different applications/systems. Its primary function is to decouple producers,
the applications that send data to brokers. Message broker acts as a mediator ensuring that messages are delivered efficiently from producers to consumers.

<img width="1062" alt="Screenshot 2024-08-24 at 12 44 50 PM" src="https://github.com/user-attachments/assets/46a198a2-72f9-497a-93c0-ae9fb8ac9873">

### Characteristics:
- Decoupling: Message Broker enables loose coupling between applications by allowing them to communicate without needing to be aware of each other's existence.
- The left-hand side sends messages to the broker & right-hand side consumes messages from the broker.
- Message Brokers often support asynchronous communication that allows producers & consumers to operate independently of each other's timing & availability.
- Scalability: Message brokers can handle large volumes of messages & scale horizontally to accommodate growing workloads
- Reliability: Reliability even in the case of system failures.

# Apache Kafka
It is a distributed, fault-tolerant & highly scalable message broker & stream processing platform. It was originally developed by LinkedIn & later open-sourced by an Apache software 
foundation project. It is designed to handle large volumes of data streams in real time in a fault-tolerant manner.

<img width="1022" alt="Screenshot 2024-08-24 at 1 16 48 PM" src="https://github.com/user-attachments/assets/02db82de-6424-4a74-8dd6-753ca2a23423">

### Key components of Kafka
- Producer: Application that publishes messages to a Kafka topic.
- Consumer: Application that subscribes to a Kafka topic & processes the published message.
- Broker: Core of the Kafka cluster. It stores & manages a stream of records.
- Topics: Topics in Kafka are used to categorize messages. Topics are divided into partitions allowing Kafka to parallelize processing & scale horizontally.
- ZooKeeper: Kafka relies on Apache ZooKeeper for distribution & management of the Kafka cluster. Its primary role is to manage the brokers. 

### Advantages
- Kafka can scale horizontally by adding more Brokers to the cluster providing high throughput & low latency in Data processing.
- Durability: Messages in Kafka are processed to disk providing their ability even during Node failure events.
- Fault Tolerant: It is designed to be tolerant ensuring that it can continue to operate seamlessly even during hardware or software failures.
- It allows for real-time stream processing making it suitable for applications that require low latency in data delivery.
- Decoupling: Kafka topic-based architecture enables the coupling between producers & consumers allowing flexibility & independence in application development
- Data Retention: Kafka provides configurable Data retention policies allowing organizations to retain messages for a specific period.
- Ecosystem integration. Kafka has a rich ecosystem with connectors for integrating with various data storage systems, stream processing frameworks & analytics tools. 

## Kafka Components

* Kafka Cluster:

  <img width="1058" alt="Screenshot 2024-08-24 at 1 36 18 PM" src="https://github.com/user-attachments/assets/cb0431cf-fc91-4fe7-bc1e-ef86e53da6b5">
  <img width="1088" alt="Screenshot 2024-08-24 at 1 45 55 PM" src="https://github.com/user-attachments/assets/1f22dbd7-d658-470d-a86e-8db7b9776721">

* Kafka Producer:

  <img width="1081" alt="Screenshot 2024-08-24 at 1 47 21 PM" src="https://github.com/user-attachments/assets/fcb05506-46f7-4287-a2c6-483fc55fe5c8">

* Kafka Consumer: Consumers can be part of a consumer group allowing them to parallelize the processing of messages.

  <img width="1083" alt="Screenshot 2024-08-24 at 1 48 27 PM" src="https://github.com/user-attachments/assets/90534f34-8494-41b7-82ba-f2021d31fa1a">

* Kafka Topics: In Apache Kafka, a topic is a fundamental abstraction that represents a category/feed name to which records/messages are published by producers & from which messages are
  consumed by consumers. Topics play a crucial role in organizing/categorizing the flow of data within a Kafka cluster. They provide a way to structure & manage data streams allowing for
  the separation of concerns in a distributed & scalable manner.

  <img width="1064" alt="Screenshot 2024-08-24 at 1 49 53 PM" src="https://github.com/user-attachments/assets/d255b55b-c489-4059-b0ec-e1f3a5236033">

  In Apache Kafka, a partition is the basic unit of parallelism & scalability. It is a way of horizontally dividing a topic into multiple independently managed units. Each partition is
  a strictly ordered linear sequence of records & it plays a crucial role in the distribution, parallel processing & fault tolerance of data within a Kafka cluster.

  <img width="1066" alt="Screenshot 2024-08-24 at 1 54 49 PM" src="https://github.com/user-attachments/assets/6e76f6c4-f36b-4302-9e12-9045af78d063">






