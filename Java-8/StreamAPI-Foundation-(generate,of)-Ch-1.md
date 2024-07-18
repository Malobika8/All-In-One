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

### Lambda

<img width="1135" alt="Screenshot 2024-07-18 at 1 28 51 PM" src="https://github.com/user-attachments/assets/0ff0ee7f-6d23-4287-9da0-bd44ac85be67">
<img width="865" alt="Screenshot 2024-07-18 at 1 28 59 PM" src="https://github.com/user-attachments/assets/794789a2-cde5-4ee5-8c5e-2ba2fea668af">

Let's try to make our code cleaner and more readable. StreamAPI lets us write clean code.

We can write the previous code in this way,

<img width="725" alt="Screenshot 2024-07-18 at 1 32 18 PM" src="https://github.com/user-attachments/assets/987825cd-5506-469a-ba38-51c4d6a075c4">

Let's try to modify it with lambda. In Lambda, we don't need to write the method name since it acts on the functional interface and already knows which method to make use of (since functional interfaces have only one abstract method).

<img width="752" alt="Screenshot 2024-07-18 at 1 35 09 PM" src="https://github.com/user-attachments/assets/b266e007-1cf7-4572-bbe5-5313050e22eb">
<img width="761" alt="Screenshot 2024-07-18 at 1 35 23 PM" src="https://github.com/user-attachments/assets/72b43abc-5a8a-4251-8397-a10961c1d070">

We can make it even shorter. We don't need to add curly braces for one line code.

<img width="1027" alt="Screenshot 2024-07-18 at 1 36 03 PM" src="https://github.com/user-attachments/assets/456d4e25-d65f-48e0-a7db-24a695fe4c06">

The *Stream.of()* method is currently returning us a Stream of Integers, So, we don't need to mention the type as *forEach()* method would get integers.

<img width="1031" alt="Screenshot 2024-07-18 at 1 38 02 PM" src="https://github.com/user-attachments/assets/e1d7b6cb-fe91-4c9f-918f-0dc579908d2d">

### Note: To deal with StreamAPI-related methods, we need to be aware of Lambda.

<img width="894" alt="Screenshot 2024-07-18 at 1 41 19 PM" src="https://github.com/user-attachments/assets/70fb3215-3a1d-435f-ac90-1035b2d1458f">
<img width="951" alt="Screenshot 2024-07-18 at 1 44 15 PM" src="https://github.com/user-attachments/assets/38fffbd7-cf03-4eac-a4d9-4d27dbe2f86c">
<img width="1009" alt="Screenshot 2024-07-18 at 2 23 32 PM" src="https://github.com/user-attachments/assets/4bd5c2ba-b832-42d7-b133-8240989c0d32">

## Using Collection as a Stream source

Consider a Student class (Create getter, setters, constructor, toString).

<img width="775" alt="Screenshot 2024-07-18 at 2 25 44 PM" src="https://github.com/user-attachments/assets/17e496f3-7812-41a8-ab14-42985f5d12e7">

We want to print a list of Students to console. This List/Collection is a source and we can get the stream of Students using
*list.stream()*

<img width="988" alt="Screenshot 2024-07-18 at 2 30 50 PM" src="https://github.com/user-attachments/assets/5c7eaf20-e12e-455c-ba79-ac045bcc50ce">

#### Output

<img width="731" alt="Screenshot 2024-07-18 at 2 31 02 PM" src="https://github.com/user-attachments/assets/b2e8483a-f14a-445b-b9a5-418b65668eff">

*Note: **stream** is not a Data Structure. It just creates a pipeline.*

<img width="994" alt="Screenshot 2024-07-18 at 2 32 08 PM" src="https://github.com/user-attachments/assets/bdf5c5e0-e409-48f2-9fb5-9bedaabf7fa6">
<img width="985" alt="Screenshot 2024-07-18 at 2 32 35 PM" src="https://github.com/user-attachments/assets/f5de95ee-550f-49a6-8dae-6c6c0f84b224">

## Assignment

<img width="795" alt="Screenshot 2024-07-18 at 2 24 38 PM" src="https://github.com/user-attachments/assets/3d212123-3081-4724-ad22-a51fe97bbe90">












