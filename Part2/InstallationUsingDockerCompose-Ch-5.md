# Kafka installation using Docker compose

In order to install Kafka on a Docker container, we need an instance of Zookeeper & an instance of Kafka. We need to create a docker-compose.yml file and define the zookeeper service & Kafka service.

1. Create a "docker-compose.yml" file.
2. Add services: We need to add images of the service. We can get the image name by Google search.

   <img width="1436" alt="Screenshot 2024-08-29 at 9 15 54 AM" src="https://github.com/user-attachments/assets/86288c83-389a-42d3-b120-1968d2a564a6">
   <img width="1434" alt="Screenshot 2024-08-29 at 9 16 33 AM" src="https://github.com/user-attachments/assets/4994d4a7-dbdd-4567-9cb9-1155aec957f3">

   We also need to tell the environment (in Kafka) where the zookeeper is running.

   <img width="1375" alt="Screenshot 2024-08-29 at 8 43 55 AM" src="https://github.com/user-attachments/assets/a3b15178-df08-44ad-bd54-3f9fe40427cf">

   We can simple use "*bitnami/kafka*" in image section rather than "*docker.io/bitnami/kafka*".

   ### Note: Use bitnami kafka & zookeeper in m1/m2 devices. See README for more details.

Once we create the docker-compose.yml file, we can execute it using the docker-compose command.

If we install the docker plugin in Intellij, we can individually run the services as well.

<img width="1147" alt="Screenshot 2024-08-27 at 11 26 38 AM" src="https://github.com/user-attachments/assets/a5677ec3-a369-4346-a87f-c5f48a5a74b3">

# Run

To run -> Go to the folder -> open terminal

Run command,

```
docker compose -f docker-compose.yml up -d
```

```
(-f: file name, -d: run in the background)
```

<img width="1353" alt="Screenshot 2024-08-27 at 11 32 22 AM" src="https://github.com/user-attachments/assets/39e9cc81-5b20-4bf9-81a9-ee87eef35ece">
<img width="1224" alt="Screenshot 2024-08-27 at 11 32 28 AM" src="https://github.com/user-attachments/assets/087f47bd-0b78-48b2-bec1-f3beb296fbbf">
<img width="1402" alt="Screenshot 2024-08-27 at 11 32 55 AM" src="https://github.com/user-attachments/assets/94c4f43f-1275-4332-8c33-04094b11e9a6">
<img width="1400" alt="Screenshot 2024-08-27 at 11 34 19 AM" src="https://github.com/user-attachments/assets/83ac6c99-0efa-4bca-a9df-8644cf7e2059">

We can check if the instances are running or not with "docker ps" command.

<img width="1398" alt="Screenshot 2024-08-29 at 9 25 01 AM" src="https://github.com/user-attachments/assets/f9cd6efc-89b6-4c9a-a1ce-b2d8888d28c5">

## Execute a bash shell (/bin/bash) inside a running Docker container

```
docker exec -it kafka /bin/sh
```
<img width="1406" alt="Screenshot 2024-08-29 at 8 44 07 AM" src="https://github.com/user-attachments/assets/25b34add-adab-4735-bf63-a5f0e8e33bfb">

## Create a Topic 

Go to kafka folder

<img width="1376" alt="Screenshot 2024-08-29 at 8 44 23 AM" src="https://github.com/user-attachments/assets/31adf039-6898-4456-8c04-ea3ecdf18044">
<img width="1367" alt="Screenshot 2024-08-29 at 8 44 56 AM" src="https://github.com/user-attachments/assets/2438b979-b3bf-44c4-a624-e69e953958f8">
<img width="1399" alt="Screenshot 2024-08-29 at 8 45 27 AM" src="https://github.com/user-attachments/assets/7917a78e-7303-4fd6-9078-6ad357f011f7">
<img width="1400" alt="Screenshot 2024-08-29 at 8 45 58 AM" src="https://github.com/user-attachments/assets/309625ec-c397-4d3e-9636-4c7ec95b197c">
<img width="1390" alt="Screenshot 2024-08-29 at 8 46 51 AM" src="https://github.com/user-attachments/assets/84d94fd4-e0d6-4c54-8c9b-7f41ca2493a6">

```
kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic quickstart
```

<img width="1398" alt="Screenshot 2024-08-29 at 9 01 32 AM" src="https://github.com/user-attachments/assets/c7d54a33-c76b-4f03-8ce6-c60b58495fbb">

## Publish messages to a topic

```
kafka-console-producer.sh --topic quickstart --bootstrap-server localhost:9092
```

<img width="1386" alt="Screenshot 2024-08-29 at 9 07 34 AM" src="https://github.com/user-attachments/assets/c475a453-4e20-496e-936c-b0cfcfc40e30">
<img width="1185" alt="Screenshot 2024-08-29 at 9 08 43 AM" src="https://github.com/user-attachments/assets/7c881b23-3320-41d8-a2e2-629a84f519e2">

## Start consumer so that it can read whatever has been published on the topic

```
kafka-console-consumer.sh --topic quickstart --from-beginning --bootstrap-server localhost:9092
```

Go to the kafka folder,

<img width="1400" alt="Screenshot 2024-08-29 at 9 10 19 AM" src="https://github.com/user-attachments/assets/a7f31878-ea30-4e27-80dd-221b88fb80f4">
<img width="1397" alt="Screenshot 2024-08-29 at 9 12 28 AM" src="https://github.com/user-attachments/assets/e7f58a61-96c9-45d6-a7dd-271247d6ceb4">

