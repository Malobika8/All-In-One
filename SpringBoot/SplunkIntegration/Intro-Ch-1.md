# Introduction

## What is Splunk?

<img width="1000" alt="Screenshot 2024-07-29 at 11 49 30 AM" src="https://github.com/user-attachments/assets/b5acc2f6-2e23-4195-9ec8-9e3301b768bc">

Splunk provides us with a User Interface using which we can filter out specific logs to Microservices. We can set alerts and monitor whole application logs directly using Splunk Dashboard.

It is used for:
- Operational Intelligence
- Data Visualisation
- Alerting
- Reporting
- Investigation

## Benefits of Splunk

<img width="1075" alt="Screenshot 2024-07-27 at 10 17 08 PM" src="https://github.com/user-attachments/assets/a0b17bc8-90eb-4a32-b42b-83fd7f38a2f9">

## Main phases of Splunk

<img width="1004" alt="Screenshot 2024-07-27 at 10 18 13 PM" src="https://github.com/user-attachments/assets/e7385fe6-d589-4cce-b95b-cae650a2556b">

## How does it work?

<img width="1062" alt="Screenshot 2024-07-27 at 10 18 27 PM" src="https://github.com/user-attachments/assets/8262d07d-9ca0-4e61-a35d-57e4e659c981">
<img width="795" alt="Screenshot 2024-07-29 at 12 11 33 PM" src="https://github.com/user-attachments/assets/bedc44bf-2f39-4eae-9100-85b5a066e8db">

- Indexer: Categorizes & applies meta-data to the data.
- Search Heads: Acts as the User Interface & allows users to create alerts, reports & dashboards based on data.

Splunk can also be trained to understand patterns. Next time onwards, it can detect patterns that can be used for visualization.

<img width="1014" alt="Screenshot 2024-07-29 at 12 15 55 PM" src="https://github.com/user-attachments/assets/042da0f9-0017-4113-b609-ac9be33fa0e0">
<img width="853" alt="Screenshot 2024-07-29 at 12 16 04 PM" src="https://github.com/user-attachments/assets/3375c0fa-36cc-4f5b-89c7-f1a75cadb350">

## Splunk Deployment models

We need to understand the Basic components of Splunk deployment.

<img width="1035" alt="Screenshot 2024-07-29 at 12 20 33 PM" src="https://github.com/user-attachments/assets/31584437-92e7-4d7f-849c-c281d94d9960">

Forwarder can forward to "Indexer" or "Indexer+Search Head" combination.

There's a "Universal forwarder" that requires very little configuration & "heavy forwarder" that can be fine-tuned as per our needs.

No matter what the configuration is, the data pipeline has four main components.
- Input
- Parsing
- Indexing
- Searching

Each of the primary components takes a part in the Data Pipeline.

<img width="1009" alt="Screenshot 2024-07-29 at 12 26 31 PM" src="https://github.com/user-attachments/assets/8a4879f3-af49-44f8-9dc6-261a7febd0ee">

### Deployment models
- Departmental deployment model: Up to 10 systems forwarding data into the search head/indexer.

  <img width="1028" alt="Screenshot 2024-07-29 at 12 28 52 PM" src="https://github.com/user-attachments/assets/184d1bed-89e3-4a1c-ac7b-43f353c3a9f3">

- Small Enterprise Deployment model:

  <img width="999" alt="Screenshot 2024-07-29 at 12 30 29 PM" src="https://github.com/user-attachments/assets/207f3314-1103-4497-9da7-52aef9cf1bda">

- Large Enterprise Deployment model:

  <img width="1040" alt="Screenshot 2024-07-29 at 12 31 11 PM" src="https://github.com/user-attachments/assets/7314d005-c422-4097-ac49-ccc6a203f837">

- Distributed Deployment: Different classes of servers i.e. linux & windows.

  <img width="1037" alt="Screenshot 2024-07-29 at 12 32 53 PM" src="https://github.com/user-attachments/assets/87eb124e-99c1-4518-8bc4-e44d1730221e">

### License

<img width="1068" alt="Screenshot 2024-07-29 at 12 35 26 PM" src="https://github.com/user-attachments/assets/a73fb9d8-77da-4887-9814-93c1440b3c0d">
<img width="1064" alt="Screenshot 2024-07-29 at 12 35 40 PM" src="https://github.com/user-attachments/assets/a04ad081-bb5c-4525-93b0-52039f95ae48">

## Metadata

<img width="1009" alt="Screenshot 2024-07-29 at 12 42 52 PM" src="https://github.com/user-attachments/assets/418a29e7-a65d-454d-aae9-604f8b5c3058">

### FYI

Splunk can consume a lot of different types of Data

<img width="855" alt="Screenshot 2024-07-29 at 12 41 16 PM" src="https://github.com/user-attachments/assets/b97eb437-c401-4bce-bfce-b22d0b86d95b">



















   


   





   














   
