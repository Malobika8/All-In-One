# Kafka installation using Docker compose

In order to install Kafka on a Docker container, we need an instance of Zookeeper & an instance of Kafka. We need to create a docker-compose.yml file and define the zookeeper service & Kafka service.

1. Create a "docker-compose.yml" file.
2. Add services: We need to add images of the service. We can get the image name by Google search.

   <img width="1436" alt="Screenshot 2024-08-27 at 11 18 20 AM" src="https://github.com/user-attachments/assets/21a7efd9-f6b2-4f60-a940-fcd84d402358">
   <img width="1434" alt="Screenshot 2024-08-27 at 11 19 02 AM" src="https://github.com/user-attachments/assets/858622c2-bea1-4c10-a47e-262c8fcc6324">

   We also need to tell the environment (in Kafka) where the zookeeper is running.

   <img width="1130" alt="Screenshot 2024-08-27 at 11 23 08 AM" src="https://github.com/user-attachments/assets/a5eddbb0-8f9d-40a5-b087-8bd0e2714eb9">

Once we create the docker-compose.yml file, we can execute it using the docker-compose command.

If we install the docker plugin in Intellij, we can individually run the services as well.

<img width="1147" alt="Screenshot 2024-08-27 at 11 26 38 AM" src="https://github.com/user-attachments/assets/a5677ec3-a369-4346-a87f-c5f48a5a74b3">

# Run

To run -> Go to the folder -> do "docker compose -f docker-compose.yml up -d"

```
(-f: file name, -d: run in the background)
```

<img width="1353" alt="Screenshot 2024-08-27 at 11 32 22 AM" src="https://github.com/user-attachments/assets/39e9cc81-5b20-4bf9-81a9-ee87eef35ece">
<img width="1224" alt="Screenshot 2024-08-27 at 11 32 28 AM" src="https://github.com/user-attachments/assets/087f47bd-0b78-48b2-bec1-f3beb296fbbf">
<img width="1402" alt="Screenshot 2024-08-27 at 11 32 55 AM" src="https://github.com/user-attachments/assets/94c4f43f-1275-4332-8c33-04094b11e9a6">
<img width="1400" alt="Screenshot 2024-08-27 at 11 34 19 AM" src="https://github.com/user-attachments/assets/83ac6c99-0efa-4bca-a9df-8644cf7e2059">

We can check if the instances are running or not with "docker ps" command.

<img width="1362" alt="Screenshot 2024-08-27 at 11 54 49 AM" src="https://github.com/user-attachments/assets/1ba607af-afb2-4437-8684-fc498e988ef5">

## Create a topic

Execute a bash shell (/bin/bash) inside a running Docker container

```
docker exec -it 8656335d1238 /bin/bash
```

create topic 

```
kafka-topic.sh --create --zookeeper zookeeper:2181 --replication-factor 1 --partition 1 --topic quickstart
```



