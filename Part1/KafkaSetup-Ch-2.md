# Setup

## Step 1: Get Kafka
- Go to https://kafka.apache.org/
- Go to quickstart & download
- Unzip it (Rename it to kafka_server for ease)

## Step 2: Start the Kafka environment

*NOTE: Your local environment must have Java 8+ installed.*

Apache Kafka can be started using KRaft or ZooKeeper. 

Run the following commands in order to start all services in the correct order: (Open a terminal at kafka_server folder)

```
# Start the ZooKeeper service
$ bin/zookeeper-server-start.sh config/zookeeper.properties
```

Open another terminal(in kafka_server folder) session and run:
```
# Start the Kafka broker service
$ bin/kafka-server-start.sh config/server.properties
```

Once all services have successfully launched, you will have a basic Kafka environment running and ready to use.

The default port is 9092.

<img width="1372" alt="Screenshot 2024-08-24 at 8 47 39 PM" src="https://github.com/user-attachments/assets/f8bd3392-df49-4dd2-932b-2f40cad6d3ac">

## Step 3: Create a topic to store your events

Kafka is a distributed event streaming platform that lets you read, write, store, and process events (also called records or messages in the documentation) across many machines.

Example events are payment transactions, geolocation updates from mobile phones, shipping orders, sensor measurements from IoT devices or medical equipment, and much more. These events are organized and stored in topics. Very simplified, a topic is similar to a folder in a filesystem, and the events are the files in that folder.

So before you can write your first events, you must create a topic. Open another terminal session and run:
```
$ bin/kafka-topics.sh --create --topic quickstart-events --bootstrap-server localhost:9092
```

<img width="1363" alt="Screenshot 2024-08-24 at 8 52 16 PM" src="https://github.com/user-attachments/assets/d7c84c20-b0a6-46bd-a5bf-50d98a91a22a">

All of Kafka's command line tools have additional options: run the kafka-topics.sh command without any arguments to display usage information. For example, it can also show you details such as the partition count of the new topic:

```
$ bin/kafka-topics.sh --describe --topic quickstart-events --bootstrap-server localhost:9092
```
<img width="1435" alt="Screenshot 2024-08-24 at 8 55 42 PM" src="https://github.com/user-attachments/assets/1a1d7738-c4b9-40f4-a6e0-8dd7b3fb7857">

## Step 4: Write some events into the topic

Let's try to push some events or write some messages to our broker by pushing them to these topics.

A Kafka client communicates with the Kafka brokers via the network for writing (or reading) events. Once received, the brokers will store the events in a durable and fault-tolerant manner for as long as you need—even forever.

Run the console producer client to write a few events into your topic. By default, each line you enter will result in a separate event being written to the topic.
```
$ bin/kafka-console-producer.sh --topic quickstart-events --bootstrap-server localhost:9092
>This is my first event
>This is my second event
```
You can stop the producer client with Ctrl-C at any time.

<img width="1377" alt="Screenshot 2024-08-24 at 9 02 17 PM" src="https://github.com/user-attachments/assets/d7e2dc93-7390-4349-a6b2-14642f22aeb9">

## Step 5: Read the events
Open another terminal session and run the console consumer client to read the events you just created:
```
$ bin/kafka-console-consumer.sh --topic quickstart-events --from-beginning --bootstrap-server localhost:9092
This is my first event
This is my second event
```
You can stop the consumer client with Ctrl-C at any time.

Feel free to experiment: for example, switch back to your producer terminal (previous step) to write additional events, and see how the events immediately show up in your consumer terminal.

Because events are durably stored in Kafka, they can be read as many times and by as many consumers as you want. You can easily verify this by opening yet another terminal session and re-running the previous command again.

<img width="1386" alt="Screenshot 2024-08-24 at 9 04 08 PM" src="https://github.com/user-attachments/assets/0d6cbf60-2049-44de-b7d6-a0016cc4aaf1">
<img width="1138" alt="Screenshot 2024-08-24 at 9 04 43 PM" src="https://github.com/user-attachments/assets/9ac8f80d-5242-4c3b-9a0d-74dea6f155f0">

### Step 8: Terminate the Kafka environment

- Stop the producer and consumer clients with Ctrl-C, if you haven't done so already.
- Stop the Kafka broker with Ctrl-C.
- Lastly, if the Kafka with ZooKeeper section was followed, stop the ZooKeeper server with Ctrl-C.
  
If you also want to delete any data of your local Kafka environment including any events you have created along the way, run the command:

```
$ rm -rf /tmp/kafka-logs /tmp/zookeeper /tmp/kraft-combined-logs
```

### Close Kafka server & then ZooKeeper

## Note

There are multiple other things that can be done.

To know more, check - https://kafka.apache.org/quickstart#quickstart_kafkaconnect





