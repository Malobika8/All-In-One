# Introduction

Stream API helps us in processing the data that flows through our Application. It was first introduced in Java 1.8.
Stream API helps us to set up a pipeline to process the Data.

### *generate()*

Let's try to generate some data first so that we can process it using Stream API. We can use a method called "generate()" provided by the StreamAPI.

### But what kind of method do we want to generate?

We can specify that. *generate()* method takes a "Supplier".

<img width="645" alt="Screenshot 2024-07-17 at 9 23 33 PM" src="https://github.com/user-attachments/assets/9233bf26-5415-4e9c-9c0b-936fa70d3e4c">
<img width="760" alt="Screenshot 2024-07-17 at 9 29 51 PM" src="https://github.com/user-attachments/assets/e19f905c-1796-4585-8b2e-14000d56a7af">

*Supplier* is a functional Interface (Every functional interface has one abstract method). Supplier has one abstract method i.e. *get()*.

<img width="1043" alt="Screenshot 2024-07-17 at 9 30 48 PM" src="https://github.com/user-attachments/assets/8a83c902-4489-4c84-a03f-87f1d5ef393a">

The *get()* method returns us something.

Let's try to provide an implementation for this.

*generate()* method gets data from *Supplier* & returns a *Stream*.

<img width="1133" alt="Screenshot 2024-07-17 at 9 34 06 PM" src="https://github.com/user-attachments/assets/07987841-f657-4c6e-9954-5ecc1fa2653d">
<img width="700" alt="Screenshot 2024-07-17 at 9 34 57 PM" src="https://github.com/user-attachments/assets/10bce442-e0bd-4be4-87a7-7ed47738d5e4">
<img width="1072" alt="Screenshot 2024-07-17 at 9 36 35 PM" src="https://github.com/user-attachments/assets/9d8228ad-6889-4da5-84dd-e7c7230060c5">

We can consume and do different tasks for each Object that comes through the Stream.

*forEach()* method helps us consume the Object.

<img width="834" alt="Screenshot 2024-07-17 at 9 39 35 PM" src="https://github.com/user-attachments/assets/7b28656b-4d13-4d85-aeea-1f7761a62160">

We need to provide an implementation of *Consumer*. It is again a Functional Interface having an *accept()* method.

<img width="1090" alt="Screenshot 2024-07-17 at 9 42 06 PM" src="https://github.com/user-attachments/assets/1f892f42-5d02-4de6-91bf-8a0233d312ef">
<img width="1049" alt="Screenshot 2024-07-17 at 9 43 12 PM" src="https://github.com/user-attachments/assets/8f696796-a14c-446b-952c-ae9b6b5881bf">

It will keep on printing the Stream. This is because the *generate()* method keeps on generating whatever is supplied to it.

<img width="1133" alt="Screenshot 2024-07-17 at 9 44 15 PM" src="https://github.com/user-attachments/assets/39a6afcf-1f67-4c74-9b2e-28e42ec53924">

<img width="1114" alt="Screenshot 2024-07-17 at 9 45 59 PM" src="https://github.com/user-attachments/assets/afddb8e1-e7df-477c-8b0a-43b6932b4c50">
<img width="1113" alt="Screenshot 2024-07-17 at 9 46 04 PM" src="https://github.com/user-attachments/assets/388e73a8-c9e7-4078-8afa-413140b9ea1a">

### *of()*

<img width="1097" alt="Screenshot 2024-07-17 at 9 46 10 PM" src="https://github.com/user-attachments/assets/bf687580-0ba4-4786-8d8b-3c41c1d5b2dd">

It returns a Stream of Objects. It doesn't generate an infinite stream though.

<img width="1155" alt="Screenshot 2024-07-17 at 9 49 02 PM" src="https://github.com/user-attachments/assets/5596be47-f2a3-4bcd-b7d4-0b1fe7abc1bd">
<img width="720" alt="Screenshot 2024-07-17 at 9 49 43 PM" src="https://github.com/user-attachments/assets/45476571-4a12-448b-a229-fd6c55220921">

<img width="1149" alt="Screenshot 2024-07-17 at 9 50 57 PM" src="https://github.com/user-attachments/assets/0c4623a7-0d7d-4126-9b31-93479959cf0a">
<img width="1136" alt="Screenshot 2024-07-17 at 9 51 04 PM" src="https://github.com/user-attachments/assets/929b2d5a-f20d-466a-9b0e-8f9428f24352">






