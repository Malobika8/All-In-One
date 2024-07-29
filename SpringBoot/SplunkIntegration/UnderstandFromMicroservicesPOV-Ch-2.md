### Let's understand how it helps us in MicroServices Architecture

Suppose we have multiple microservices. to track any issue from every service, we need to monitor logs. Traditionally, all logs are captured by a single log file which is a bad practice/design.

<img width="1090" alt="Screenshot 2024-07-29 at 11 53 43 AM" src="https://github.com/user-attachments/assets/de2ebe85-b7aa-43fc-8eb2-a2d05866b552">

Suppose an issue occurs in "inventory-service", we would need to debug whole logs to identify the issue which takes a huge amount of time to filter out specific flow of "inventory-service" logs.

Splunk helps in segregating whole logs by creating an index. We can create indexes for each microservices. We can forward service-specific logs to Splunk using specific indexes. 

This helps in segregating entire logs specific to each microservice. Now if an issue occurs to any of the services, we can simply search logs with that specific index which will get us service data which is much easier to debug.

<img width="1094" alt="Screenshot 2024-07-29 at 11 56 46 AM" src="https://github.com/user-attachments/assets/07df1edf-256d-4899-86c6-41fcd1ed0d03">

## How to forward application logs to Splunk using indexes?

- Use any logging framework in the application
- Once we capture the logs of our application, forward it to Splunk.

## How does our application connect to Splunk?

Both run on different servers. We need to tell our application where our Splunk server is running and the various properties that are required to connect to it.

<img width="951" alt="Screenshot 2024-07-29 at 12 01 51 PM" src="https://github.com/user-attachments/assets/dfe64c40-63fa-40d6-a93f-de00a75b37c0">

We can configure it by creating a log file depending on the logging framework used on the application & then by providing necessary information.

<img width="1005" alt="Screenshot 2024-07-29 at 12 03 34 PM" src="https://github.com/user-attachments/assets/11a8fa25-1f47-4eda-8d55-d4189ba11925">


