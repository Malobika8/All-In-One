# SQL

## Agenda

<img width="869" alt="Screenshot 2024-07-24 at 8 10 30 PM" src="https://github.com/user-attachments/assets/f6690e1b-8086-4035-b7e9-0701b06754d2">

**SQL** - *Structured Query Language (Language to interact with the Database)*

**Database** - *A place where we store/organize our Data (Example: Google Drive).*

<img width="807" alt="Screenshot 2024-07-24 at 8 21 21 PM" src="https://github.com/user-attachments/assets/b2262f1a-9f17-4c4a-a19a-88eaa6f4a96c">

To deal with these kinds of Data, we use something called a "**Database**". It is itself divided into smaller parts called "**Tables**".

### Types of Databases(based on the kind of data stored)

* Relational Database: Where we store Data in the form of Tables - SQL helps us to work with Relational Databases.
* Non-Relational Database:  Data is not stored in the form of Tables. We can store in other forms like Document format, key-value pair, JSON, etc. - MongoDB, Cassandra, NoSQL, etc 
  helps us work with Non-Relational Database.

<img width="764" alt="Screenshot 2024-07-24 at 8 37 48 PM" src="https://github.com/user-attachments/assets/3f2c8571-b9f8-49a0-adc4-c3285527d20a">
<img width="763" alt="Screenshot 2024-07-24 at 8 40 57 PM" src="https://github.com/user-attachments/assets/cc7416eb-1639-4925-9838-b74c0103a493">
<img width="767" alt="Screenshot 2024-07-24 at 8 41 12 PM" src="https://github.com/user-attachments/assets/b13a7629-eb86-408b-a17c-207d5220c870">

#### Applications: CRUD operations- Create, Read, Update, Delete

### SQL Structure

<img width="764" alt="Screenshot 2024-07-24 at 8 41 37 PM" src="https://github.com/user-attachments/assets/660df8c9-bf90-4d2e-b2f0-db051b19b5e5">

### There are 5 types of SQL Commands:

* Data Definition Language (DDL) – to define and modify the structure of a database.
* Data Manipulation Language (DML) – to access, manipulate, and modify data in a database.
* Data Control Language (DCL) – to control user access to the data in the database and give or revoke privileges to a specific user or a group of users.
* Transaction Control Language (TCL) – to control transactions in a database.
* Data Query Language (DQL) – to perform queries on the data in a database to retrieve the necessary information from it.
  
#### Consider the following Database diagram/schema. (Schema tells us how different things are connected to each other)

<img width="770" alt="Screenshot 2024-07-24 at 8 42 25 PM" src="https://github.com/user-attachments/assets/1d437d3a-d483-4de5-8f44-3625be07b4b3">

"id" would help us to identify the Order ("orders" table) uniquely. Hence, "id" can be considered the primary key.

We can see that "order_id"(primary key) in the "order_items" table is connected to "id" in the "orders" table. Technically, "order_id" & "id" are the same. In this scenario, "order_id" would act as a *foreign key* to the "orders" table as it creates a connection to the "orders" table. Similarly, "id" in the "orders" table would act as a foreign key to the "order_items" table.

### Sample "create" query

<img width="933" alt="Screenshot 2024-07-24 at 9 06 49 PM" src="https://github.com/user-attachments/assets/0d0aed38-e2bc-424d-862b-8728ca27d9ad">

### Sample "insert" query

<img width="860" alt="Screenshot 2024-07-24 at 9 10 29 PM" src="https://github.com/user-attachments/assets/2033f4db-522e-4c20-8d9d-0cd0f49daf5f">

### Sample "select" query

<img width="883" alt="Screenshot 2024-07-24 at 9 13 47 PM" src="https://github.com/user-attachments/assets/a553256f-fa4a-457b-a16d-b96ecd7c9841">

### Sample "update" query

<img width="849" alt="Screenshot 2024-07-24 at 9 17 19 PM" src="https://github.com/user-attachments/assets/943e3b68-acd6-44ce-b6bb-3e7f852fe21c">
<img width="881" alt="Screenshot 2024-07-24 at 9 18 03 PM" src="https://github.com/user-attachments/assets/284b89cf-8b55-4546-8ba3-1bab74f88a55">

### Sample "alter" query

<img width="878" alt="Screenshot 2024-07-24 at 9 20 34 PM" src="https://github.com/user-attachments/assets/e0b62b9f-3a89-4277-b378-6077d7a8b438">
<img width="874" alt="Screenshot 2024-07-24 at 9 20 46 PM" src="https://github.com/user-attachments/assets/6b0bc611-74b8-464b-8ad2-94bc3ccf9934">

### Sample "delete" query

<img width="848" alt="Screenshot 2024-07-24 at 9 22 03 PM" src="https://github.com/user-attachments/assets/dd84b783-a7a2-40cb-abd9-d2969d6c73fe">
<img width="877" alt="Screenshot 2024-07-24 at 9 23 09 PM" src="https://github.com/user-attachments/assets/e3608174-4db7-48bc-b2e1-ae213d7c8e0a">

### Example 

Consider another table "classroom20"

<img width="880" alt="Screenshot 2024-07-24 at 9 26 34 PM" src="https://github.com/user-attachments/assets/25d70a72-e4bb-4174-a0c6-dc2d9d25d4dc">
<img width="879" alt="Screenshot 2024-07-24 at 9 27 03 PM" src="https://github.com/user-attachments/assets/4851531f-3e9d-43e8-b581-63a002cb0c00">

### Distinct - Find unique grades

<img width="913" alt="Screenshot 2024-07-24 at 9 28 21 PM" src="https://github.com/user-attachments/assets/95b6151c-f247-4347-a1c5-efd2c0445777">
<img width="818" alt="Screenshot 2024-07-24 at 9 28 39 PM" src="https://github.com/user-attachments/assets/9f9b4cbb-0d34-4460-bd47-5f0b26c918d5">

### Limit

<img width="919" alt="Screenshot 2024-07-24 at 9 30 03 PM" src="https://github.com/user-attachments/assets/dfcc803d-4218-42e9-978d-274fa004a0fe">
<img width="875" alt="Screenshot 2024-07-24 at 9 30 22 PM" src="https://github.com/user-attachments/assets/0ea73a94-b083-4bc2-b2f5-a766adec9a54">

### Order by Ascending and Descending order

#### Asc

<img width="893" alt="Screenshot 2024-07-24 at 9 31 06 PM" src="https://github.com/user-attachments/assets/e72937dc-7ab1-4416-b1aa-89691b6293fc">
<img width="868" alt="Screenshot 2024-07-24 at 9 33 28 PM" src="https://github.com/user-attachments/assets/56942125-746b-4ba3-af2f-3cd30bd31e4f">

#### Desc

<img width="880" alt="Screenshot 2024-07-24 at 9 36 21 PM" src="https://github.com/user-attachments/assets/9a592309-d122-40b0-8dbe-ae00cede5e0f">

### Example

Consider two tables "payment20" & "customer20"

<img width="925" alt="Screenshot 2024-07-24 at 9 38 24 PM" src="https://github.com/user-attachments/assets/27be184d-11fa-4fc0-870a-52790b87fe7d">
<img width="860" alt="Screenshot 2024-07-24 at 9 39 00 PM" src="https://github.com/user-attachments/assets/ecbf5f02-9973-4832-a4d3-2f5c88dd5dbf">
<img width="875" alt="Screenshot 2024-07-24 at 9 39 25 PM" src="https://github.com/user-attachments/assets/54d8e9b3-09fc-4fc7-904e-cd23bcd92a00">

#### Guess the output:

* Question 1:

  <img width="887" alt="Screenshot 2024-07-24 at 9 40 05 PM" src="https://github.com/user-attachments/assets/ef8a27d1-41e6-4f86-b45e-8a57bd8107bb">
  <img width="876" alt="Screenshot 2024-07-24 at 9 42 02 PM" src="https://github.com/user-attachments/assets/7bd9a461-c478-4cff-9386-f743900a7cc9">

* Question 2:

  <img width="916" alt="Screenshot 2024-07-24 at 9 46 35 PM" src="https://github.com/user-attachments/assets/2bf5fb03-c180-4357-8621-f295d3b00590">
  <img width="856" alt="Screenshot 2024-07-24 at 9 46 31 PM" src="https://github.com/user-attachments/assets/adbfb6c9-ea9e-4701-a8c5-990412b85ef7">

# FYI

<img width="896" alt="Screenshot 2024-07-24 at 9 52 30 PM" src="https://github.com/user-attachments/assets/809774bf-71e0-4351-904b-04475614b129">
<img width="871" alt="Screenshot 2024-07-24 at 9 56 16 PM" src="https://github.com/user-attachments/assets/1b51e12c-0125-4ddb-b423-4a7fc2f43882">







