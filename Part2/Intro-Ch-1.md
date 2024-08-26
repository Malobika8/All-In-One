# What is Kafka?

<img width="1091" alt="Screenshot 2024-08-26 at 10 56 53 AM" src="https://github.com/user-attachments/assets/3b005c0a-6ca8-41d5-9dba-2828eeeb6f8f">

Event Streaming points to 2 different tasks:
- Creating real-time stream
- Processing real-time stream

Let's try to nuderstand with a real life example.

Everybody uses Paytm (api payment method). Let's say we're booking movie ticket. When we do any transaction, that event goes to Kafka server. Since there are multiple users, Kafka server
receives millions of events per minute.

<img width="761" alt="Screenshot 2024-08-26 at 11 00 16 AM" src="https://github.com/user-attachments/assets/3580f8cb-f1c5-4fbc-be02-ad2606526507">

So, sending the stream of continuous data from Paytm to the Kafka server can be referred to as "Creating/Generating Real-time event stream".

Now, once Kafka server receives the data, it needs to process. There's a client aplication developed by Paytm that reads the data from Kafka server and processed it

Suppose there's a restriction that a user can do 10 transactions per day in Paytm. If the limit exceeds, a notification is sent to the user. In such a scenario, our client application
needs to continuously trace the data and need to do validation of transaction count for a specific user in each or every sec or milisecond. So, it continuously listens to the Kafka
messages and processes them. This can be referred to as "Processing real-time event stream".

<img width="1114" alt="Screenshot 2024-08-26 at 11 04 43 AM" src="https://github.com/user-attachments/assets/c598751a-4330-489d-9ea0-01a21c87eba5">

Continuously sending messages/events to the Kafka server & reading/processing them is called "**Real-time event streaming**".

In Microservices world, distributed means distributing multiple computers to different node or region to balance the load & avoid downtime. Similarly, Kafka is a distributed event
streaming platform. Kafka servers can also be distributed. If any server goes down, another picks up the traffic to avoid application downtime.

# Where does Kafka come from?

<img width="1043" alt="Screenshot 2024-08-26 at 11 13 44 AM" src="https://github.com/user-attachments/assets/a8bffbec-eba6-44d4-a755-56ac8e75b897">

# Why do we need Kafka?

Let's try to understand with the help of an example.

Let's suppose there's a person to whom a letter is to be delivered. The postman attempts to deliver the letter but couldn't because of his unavailability. The postman checks for 2-3 days
ultimately discarding the message. This could be a huge loss for the person.

#### How can this be avoided?

A letter box could be installed near the house wherein if the person is unavailable, the postman can simply put it into the letterbox. In this way, the information won't be lost.
Here, letterbox acts as middleman between postman & the person.

Let's now consider 2 application where application-1 wants to send some data to application-2. However, application-2 is unavailable. So, to avoid loss of data, something like a 
letterbox can be installed in between. This is when Kafka comes into the picture. We can add a Messaging system. This messaging system can be Kafka or RabbitMQ or Redis. So in case
application-2 is unavailabe, the message can be picked up from Kafka whenever application-2 comes online. Kafka acts as a letterbox here and helps in avoiding data loss.

Let's look at another example.

Suppose we have 4 applications that wants to store different kinds of data to Database Server. This seems simple since the application is small. 

<img width="749" alt="Screenshot 2024-08-26 at 11 28 31 AM" src="https://github.com/user-attachments/assets/9463df48-4f27-4f32-9fe4-e43ee9efacf0">

However, it might grow in future. We might have n number of services to communicate with each other. It would become really challenging to maintain communication between so many 
applications. Applications might want to send data in different formats to different systems. Also, there could be different type of connection with different systems. It would be complex 
to maintain.

<img width="1127" alt="Screenshot 2024-08-26 at 11 30 17 AM" src="https://github.com/user-attachments/assets/70d0bbc0-5fca-493d-bbad-e15a9f90245b">

To overcome this, a messaging system is required. 

<img width="1029" alt="Screenshot 2024-08-26 at 11 33 07 AM" src="https://github.com/user-attachments/assets/2257a72b-d9b4-4e4f-be3e-a73b344c4c44">

The services could simply send the payload with all different information to Kafka server and the consumers could pick up the required data from Kafka.

# How does it work? (high level overview)

It basically works on Pub/Sub model. 

Usually there are 3 components
- Publisher: Publishes the events to message broker.
- Message Broker
- Subscriber: Consumes the events from Broker. It subscribes to a specific topic and when any event related to the topic is published, subscriber consumes it.

<img width="1086" alt="Screenshot 2024-08-26 at 11 40 25 AM" src="https://github.com/user-attachments/assets/b4e7bc6c-2f1d-4d76-b859-fc0ecdbd4e62">

















