<img width="836" height="239" alt="Screenshot 2025-08-25 at 10 31 22 AM" src="https://github.com/user-attachments/assets/7bd57dd7-b318-443f-9e83-dd2697cff90f" />

# We'll be using JDBCUserDetailsManager instead of InMemoryUserDetailsManager

<img width="1100" height="382" alt="Screenshot 2025-08-25 at 10 48 44 AM" src="https://github.com/user-attachments/assets/6daeda45-e2ee-4beb-93ef-95f02fe4347e" />
<img width="873" height="422" alt="Screenshot 2025-08-25 at 10 49 19 AM" src="https://github.com/user-attachments/assets/1d5eaa5f-306e-41e1-b214-c57a8061f8a1" />

### Create a bean for the same

<img width="859" height="175" alt="Screenshot 2025-08-25 at 10 51 54 AM" src="https://github.com/user-attachments/assets/c52b84e6-c27e-434a-be29-bbb9e5dc07ab" />
<img width="1098" height="312" alt="Screenshot 2025-08-25 at 10 56 44 AM" src="https://github.com/user-attachments/assets/a2ff2ac8-55ec-47bb-9489-8e22a57ea7aa" />

### Let's try to register

<img width="645" height="197" alt="Screenshot 2025-08-25 at 10 58 05 AM" src="https://github.com/user-attachments/assets/e293bf09-9ea9-4ca3-8dfd-fa36a721b7ca" />
<img width="1081" height="226" alt="Screenshot 2025-08-25 at 10 58 12 AM" src="https://github.com/user-attachments/assets/1ec53157-0aa4-44de-8b84-a68a1f04a448" />

### What happens internally when we do createUser()?

<img width="865" height="71" alt="Screenshot 2025-08-25 at 10 59 56 AM" src="https://github.com/user-attachments/assets/e1695478-0aa1-4c0f-84d1-9bdc8f82342b" />
<img width="857" height="378" alt="Screenshot 2025-08-25 at 11 00 24 AM" src="https://github.com/user-attachments/assets/0d066f85-3fba-4ece-9cc3-bad31c1bce29" />
<img width="1103" height="245" alt="Screenshot 2025-08-25 at 11 00 32 AM" src="https://github.com/user-attachments/assets/e287e77f-0496-4a0a-a469-006ca1fa7508" />
<img width="1100" height="245" alt="Screenshot 2025-08-25 at 11 00 43 AM" src="https://github.com/user-attachments/assets/7f287231-b572-4f0b-8a16-036554232d69" />

### We need to create a "*users*" table with the fields mentioned

<img width="921" height="384" alt="Screenshot 2025-08-25 at 11 02 24 AM" src="https://github.com/user-attachments/assets/1fa6bd15-451e-4c0c-86d0-6fd0d05dd22d" />
<img width="863" height="362" alt="Screenshot 2025-08-25 at 11 02 34 AM" src="https://github.com/user-attachments/assets/e9a5286c-ae46-4519-b4c7-53a05561c70f" />

### Let's try to register again

<img width="502" height="330" alt="Screenshot 2025-08-25 at 11 03 47 AM" src="https://github.com/user-attachments/assets/c0d8338e-0aa8-458d-a87b-b76c1d85cb88" />
<img width="1076" height="202" alt="Screenshot 2025-08-25 at 11 04 01 AM" src="https://github.com/user-attachments/assets/64f74ce0-108f-4384-ac13-8d4055bce3d0" />

### We are encoding the password with the BCrypt encoder and storing it. It is too long. We can either increase the length or for now, move to Noop encoder.

<img width="1064" height="77" alt="Screenshot 2025-08-25 at 11 04 43 AM" src="https://github.com/user-attachments/assets/b84c206c-27f8-4f75-b858-6ef557fc2994" />
<img width="786" height="181" alt="Screenshot 2025-08-25 at 11 04 59 AM" src="https://github.com/user-attachments/assets/84d8374f-342f-4642-8207-bca4e0c52a28" />

### Let's try to register again

<img width="593" height="184" alt="Screenshot 2025-08-25 at 11 05 38 AM" src="https://github.com/user-attachments/assets/022c0bac-4d83-4a0c-891f-0a5573caebc6" />
<img width="1078" height="198" alt="Screenshot 2025-08-25 at 11 05 45 AM" src="https://github.com/user-attachments/assets/deda054b-58e7-4043-b845-757a5658a715" />

#### Although the user detail is inserted, we need another table to hold authorities.

<img width="593" height="339" alt="Screenshot 2025-08-25 at 11 06 48 AM" src="https://github.com/user-attachments/assets/1ff8333f-1a1f-455f-92df-e2e6edb8660a" />
<img width="993" height="307" alt="Screenshot 2025-08-25 at 11 07 07 AM" src="https://github.com/user-attachments/assets/4c6c6a60-c71b-4522-8328-8193dc18357f" />
<img width="1110" height="264" alt="Screenshot 2025-08-25 at 11 07 19 AM" src="https://github.com/user-attachments/assets/133bd737-8138-4c77-8b29-49348cfd1e71" />
<img width="1103" height="214" alt="Screenshot 2025-08-25 at 11 07 36 AM" src="https://github.com/user-attachments/assets/48d3341e-67c8-49ca-a7cb-cc0b60fe46b0" />
<img width="1112" height="313" alt="Screenshot 2025-08-25 at 11 07 46 AM" src="https://github.com/user-attachments/assets/dfda0b42-5069-422d-aa35-665d90d763e2" />

### Create "*authorities*" table

<img width="604" height="402" alt="Screenshot 2025-08-25 at 11 08 34 AM" src="https://github.com/user-attachments/assets/832efb15-ba05-44d8-8ddf-230357bd78eb" />
<img width="577" height="317" alt="Screenshot 2025-08-25 at 11 08 42 AM" src="https://github.com/user-attachments/assets/ba0bb757-b332-40e4-af71-693390b7fa54" />

### Let's try to register again

<img width="640" height="185" alt="Screenshot 2025-08-25 at 11 09 09 AM" src="https://github.com/user-attachments/assets/5c7f024e-3f9e-4a16-90dc-fe2696654d05" />
<img width="677" height="144" alt="Screenshot 2025-08-25 at 11 09 14 AM" src="https://github.com/user-attachments/assets/ec03d4b6-1cb5-4a64-aeb7-cbd3f990c9e4" />
<img width="576" height="325" alt="Screenshot 2025-08-25 at 11 09 32 AM" src="https://github.com/user-attachments/assets/41a9b793-956b-4c65-8820-4fc963820648" />
<img width="575" height="326" alt="Screenshot 2025-08-25 at 11 09 39 AM" src="https://github.com/user-attachments/assets/c884c9c2-e044-4be2-98e9-a1cd2f98f22c" />

#### Spring automatically inserts prefix "ROLE_" with the role provided

<img width="790" height="154" alt="Screenshot 2025-08-25 at 11 09 55 AM" src="https://github.com/user-attachments/assets/e5325cc4-b6a1-48f9-88ca-34478c207836" />
<img width="551" height="147" alt="Screenshot 2025-08-25 at 11 10 09 AM" src="https://github.com/user-attachments/assets/604c613c-8a30-428f-8392-8db6a57bb0af" />

## Note: We might come across this error if we have both InMemoryUserDetailsManager and JdbcUserDetailsManager set up.

<img width="881" height="370" alt="Screenshot 2025-08-25 at 11 11 16 AM" src="https://github.com/user-attachments/assets/42afb0e9-de88-4ab4-b4bb-c1919ed7e0e5" />
<img width="752" height="341" alt="Screenshot 2025-08-25 at 11 11 22 AM" src="https://github.com/user-attachments/assets/116ddc38-6ad8-48a3-9480-1b8cb37c1c8a" />
<img width="1141" height="523" alt="Screenshot 2025-08-25 at 11 12 20 AM" src="https://github.com/user-attachments/assets/3354b1c7-3f8f-445a-8a8c-b9aef79c6b0b" />

#### We can remove/comment the one we don't require.

<img width="859" height="465" alt="Screenshot 2025-08-25 at 11 12 56 AM" src="https://github.com/user-attachments/assets/064445ea-6a68-4661-87c3-4d3291f7406e" />

### Let's try to register again

<img width="527" height="277" alt="Screenshot 2025-08-25 at 11 13 21 AM" src="https://github.com/user-attachments/assets/aa37592f-5dd5-4dd7-b98b-239dd7cd71e3" />
<img width="747" height="123" alt="Screenshot 2025-08-25 at 11 13 31 AM" src="https://github.com/user-attachments/assets/3a7c5e96-993e-475c-920d-4a1cdc2a4944" />
<img width="915" height="301" alt="Screenshot 2025-08-25 at 11 14 03 AM" src="https://github.com/user-attachments/assets/f8f8a493-0002-4a2a-a24f-c59ad62b83a0" />
<img width="686" height="116" alt="Screenshot 2025-08-25 at 11 14 08 AM" src="https://github.com/user-attachments/assets/c89ac97d-68c4-4e7c-b074-f29d8bfbb237" />
<img width="588" height="256" alt="Screenshot 2025-08-25 at 11 14 22 AM" src="https://github.com/user-attachments/assets/31f504e4-9d49-4782-b4ae-85fb5eedb29a" />
<img width="842" height="133" alt="Screenshot 2025-08-25 at 11 14 40 AM" src="https://github.com/user-attachments/assets/8b16acc9-579f-4be1-b87e-463160032482" />

### Note that every user MUST have a role associated

<img width="896" height="110" alt="Screenshot 2025-08-25 at 11 37 14 AM" src="https://github.com/user-attachments/assets/2170790d-0910-475d-b2a5-c57a07a7a0dc" />
<img width="1063" height="244" alt="Screenshot 2025-08-25 at 11 37 34 AM" src="https://github.com/user-attachments/assets/3216cd34-6d4e-4ead-a647-95a232e8775c" />

### In the "*authorities*" table, username should never be the primary key, as each user can have multiple roles. "*users*" and "*authorities*" have a ONE-TO-MANY relationship.

<img width="529" height="183" alt="Screenshot 2025-08-25 at 11 40 35 AM" src="https://github.com/user-attachments/assets/7b62eef6-5952-41e4-aa3b-9a8ca556f3b4" />
<img width="495" height="141" alt="Screenshot 2025-08-25 at 11 40 39 AM" src="https://github.com/user-attachments/assets/a1d84214-3ce2-4d10-bdd2-b5d66b7dd85d" />
<img width="582" height="334" alt="Screenshot 2025-08-25 at 11 41 05 AM" src="https://github.com/user-attachments/assets/dafd486b-1b98-4491-8c4b-ae109bde3450" />
<img width="551" height="226" alt="Screenshot 2025-08-25 at 11 41 36 AM" src="https://github.com/user-attachments/assets/3a9c24ad-7f77-4681-a9fe-a18a5471ac5e" />

# Check out the official doc for schema declaration

<img width="1079" height="412" alt="Screenshot 2025-08-25 at 11 42 12 AM" src="https://github.com/user-attachments/assets/f0483f02-7bd6-42db-bc53-a4d28788c50b" />

