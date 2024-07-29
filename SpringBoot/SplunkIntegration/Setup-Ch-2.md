## How to forward application logs to Splunk using indexes?

- Use any logging framework in the application
- Once we capture the logs of our application, forward it to Splunk.

## How does our application connect to Splunk?

Both run on different servers. We need to tell our application where our Splunk server is running and the various properties that are required to connect to it.

<img width="951" alt="Screenshot 2024-07-29 at 12 01 51 PM" src="https://github.com/user-attachments/assets/dfe64c40-63fa-40d6-a93f-de00a75b37c0">

We can configure it by creating a log file depending on the logging framework used on the application & then by providing necessary information.

<img width="1005" alt="Screenshot 2024-07-29 at 12 03 34 PM" src="https://github.com/user-attachments/assets/11a8fa25-1f47-4eda-8d55-d4189ba11925">

# Splunk Setup

1. Search for Splunk in the browser.

   <img width="854" alt="Screenshot 2024-07-27 at 10 19 35 PM" src="https://github.com/user-attachments/assets/fa4ded33-893c-4b37-b493-e40249f35212">

2. Go to "**Product**" -> "**Splunk Enterprise**"

   <img width="1436" alt="Screenshot 2024-07-27 at 10 21 02 PM" src="https://github.com/user-attachments/assets/2653fdc5-663a-43bd-a73f-1d254ddd54a3">

3. Click on the free trial. Create an account (trial for 60 days).
4. Install Splunk & log in with username "admin" & provide the same password we used for signup.

   <img width="1436" alt="Screenshot 2024-07-27 at 10 38 54 PM" src="https://github.com/user-attachments/assets/13ad9e88-6751-404b-bf4a-9c5ce36288c1">

# Create Token & Indexes in Splunk

-  Go to "Settings" & click on "Data Input"

   <img width="713" alt="Screenshot 2024-07-27 at 10 45 05 PM" src="https://github.com/user-attachments/assets/bf436d2a-750d-4984-9589-0eb9e72b1ae6">

   We can see a lot of options but we'll be using "HTTP Event Collector"

   <img width="1172" alt="Screenshot 2024-07-27 at 10 46 11 PM" src="https://github.com/user-attachments/assets/2fb9cfc6-8d74-4393-b96b-720cee77298b">

   We have to create indexes.

   Before that, Go to "Global Settings". Port no (where our logs will be generated)

   **Note: Disable SSL**

   <img width="800" alt="Screenshot 2024-07-28 at 10 09 25 AM" src="https://github.com/user-attachments/assets/7777cfdd-a80a-48e2-8ba9-040ea1d9e6d0">

   Go to "Tokens"

   <img width="864" alt="Screenshot 2024-07-28 at 10 11 06 AM" src="https://github.com/user-attachments/assets/b8c13fb7-c36f-4d8f-9285-b815b5532756">

   Create indexes. (We can create different for different environments)

   <img width="800" alt="Screenshot 2024-07-28 at 10 13 38 AM" src="https://github.com/user-attachments/assets/a5379fe3-199f-46a8-bf57-bc134a1e37c3">

   Select "source type" where we need to log our data. (Whatever logging tool we use in our project, we need to select that)

   <img width="1164" alt="Screenshot 2024-07-28 at 10 15 23 AM" src="https://github.com/user-attachments/assets/eafebc55-1411-4bc8-abb4-ccd0e8c20014">

   We can see all the data in the review section. Save it somewhere as it'll be needed while integrating our Spring Boot application with       Splunk ( in the XML file).

   <img width="753" alt="Screenshot 2024-07-28 at 10 18 40 AM" src="https://github.com/user-attachments/assets/ab72f6e1-769e-4bb4-9050-ffcf3ab4bcba">

   Click on submit. Our token is created.

   <img width="886" alt="Screenshot 2024-07-28 at 10 19 56 AM" src="https://github.com/user-attachments/assets/a112ff72-b2ef-4358-9ff2-2f63de4fea3b">

   Click on "Start Searching".

   We can see Splunk has provided the query that can be used to search logs.

   <img width="1046" alt="Screenshot 2024-07-28 at 10 21 21 AM" src="https://github.com/user-attachments/assets/04c48635-6119-43e6-8c32-26466bbfb5eb">

   We can go to "HTTP Event Collector" & see the token created.

   <img width="1420" alt="Screenshot 2024-07-28 at 10 23 56 AM" src="https://github.com/user-attachments/assets/a769000c-7410-4d3c-a453-263dc7de5317">
