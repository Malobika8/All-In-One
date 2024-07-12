# FeignClient (OpenFeign)

*The FeignClient is a Spring Boot library that simplifies the process of creating and consuming REST clients. It provides a simple and intuitive way to create REST clients and handle 
errors and retries. The history of FeignClient dates back to 2011 when it was created by Netflix as an internal project. It was later open-sourced and became a popular Spring Boot 
dependency. Today, FeignClient is widely used in the Spring ecosystem to create efficient and scalable REST clients.*

https://github.com/OpenFeign/feign

It is a RestClient which was originally developed by Netflix. 

Netflix internally used FeignClient for a very long time & later made it OpenSource which is why they don't provide support anymore.
Netflix has open source community(Netflix OSS). As part of that, they have tons of projects that has been added in Developer community. 

Spring provides a lot of spring features on top of OpenFeign (to make it easier).

## Spring Cloud OpenFeign.
Spring Cloud OpenFeign is a declarative HTTP client library for building RESTful microservices. It integrates seamlessly with Spring Cloud and simplifies the development of HTTP clients
by allowing us to create interfaces that resemble the API of the target service.

*Feign is a declarative web service client. It makes writing web service clients easier. To use Feign create an interface and annotate it.*

```
A declarative REST client is a software component that simplifies communication between your application and a RESTful web service. It treats the call to the service as a declarative
statement, describing the operation you want to perform, rather than executing the operation itself. This allows you to abstract away the implementation details of the service, making
your code more modular and reusable. Declarative REST clients can be found in various programming languages and frameworks, enabling you to focus on your application's logic rather
than the service API's intricacies.
```

Dependencies required:

```
<!-- https://mvnrepository.com/artifact/org.springframework.cloud/spring-cloud-starter-openfeign -->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-openfeign</artifactId>
    <version>4.1.1</version>
</dependency>
```

Parent pom for spring cloud dependencies

<img width="777" alt="Screenshot 2024-07-12 at 12 37 01 PM" src="https://github.com/user-attachments/assets/2d2e2bc0-c1ae-4a9f-9f95-4cb11d7d698d">
<img width="769" alt="Screenshot 2024-07-12 at 12 36 28 PM" src="https://github.com/user-attachments/assets/9ca66c8b-a0ee-4243-9e45-b7552d575f6d">

### Rest API call using FeignClient

<img width="833" alt="Screenshot 2024-07-12 at 12 43 39 PM" src="https://github.com/user-attachments/assets/a7eff5c7-b759-4230-bee1-1548b02b6882">
<img width="945" alt="Screenshot 2024-07-12 at 12 43 59 PM" src="https://github.com/user-attachments/assets/8ab6a24b-a01f-4a30-92e2-f14fc8a4a25a">

OR 

We can simply copy the method directly from the *address-service*.

<img width="1092" alt="Screenshot 2024-07-12 at 12 56 59 PM" src="https://github.com/user-attachments/assets/a42e05d5-0bb6-4915-83a2-3c586e032033">
<img width="961" alt="Screenshot 2024-07-12 at 12 59 54 PM" src="https://github.com/user-attachments/assets/53b07735-faa4-47de-ba4a-6a92db319bd7">

We don't have to write an implementation for AddressClient. It's a proxy class. Spring does it for us.

<img width="874" alt="Screenshot 2024-07-12 at 12 46 28 PM" src="https://github.com/user-attachments/assets/c852fc09-c285-4c9c-ac06-6852d38ddf0b">
<img width="938" alt="Screenshot 2024-07-12 at 12 48 05 PM" src="https://github.com/user-attachments/assets/317d650d-e210-452f-9d32-228dd00f2cad">

----------------------------

Errors we might come across:

- Bean not found: This ideally should go away with project reload and mvn clean install

  <img width="860" alt="Screenshot 2024-07-12 at 12 49 33 PM" src="https://github.com/user-attachments/assets/402a72b3-2165-4b73-ae9e-88701c8c3c46">

- We should provide name and value to our FeignClient. Value is nothing but the Base URL.

  <img width="852" alt="Screenshot 2024-07-12 at 12 51 17 PM" src="https://github.com/user-attachments/assets/0821844e-582c-4f07-a4dc-9d725f67718b">

  We can even write this way,

  <img width="1070" alt="Screenshot 2024-07-12 at 2 54 26 PM" src="https://github.com/user-attachments/assets/fe13f413-c2ab-4503-836a-efe136c9bbd7">

----------------------------

Run the Application

<img width="940" alt="Screenshot 2024-07-12 at 12 54 35 PM" src="https://github.com/user-attachments/assets/ecca13ce-53ef-4419-8d68-29102ad4fe06">

*Note: It works for all service instances(multiple will have multiple ports).*

### Example

Calls a different method

<img width="1150" alt="Screenshot 2024-07-12 at 1 06 31 PM" src="https://github.com/user-attachments/assets/948d910b-1e60-482b-8069-95876caf602d">
<img width="1235" alt="Screenshot 2024-07-12 at 1 06 19 PM" src="https://github.com/user-attachments/assets/a1961980-3e36-428d-b11a-7d87e403a408">

Communicate with two different services

<img width="1180" alt="Screenshot 2024-07-12 at 1 08 34 PM" src="https://github.com/user-attachments/assets/3ad79b46-1775-4809-87f8-83308490bd40">
<img width="1139" alt="Screenshot 2024-07-12 at 1 08 48 PM" src="https://github.com/user-attachments/assets/6a1660b3-1795-49e2-9e01-e5ac05419b4e">
<img width="1173" alt="Screenshot 2024-07-12 at 1 08 57 PM" src="https://github.com/user-attachments/assets/8c737ea9-d64a-4519-80f0-43910c5084af">

### Why use FeignClient?
It can easily integrate with other Spring cloud Projects like Eureka, Gateway, Loadbalancer, etc.

The most compelling advantage of using @FeignClient is its declarative nature. You define an interface and annotate it with @FeignClient , and Spring takes care of the rest. You don't have to write code for HTTP calls, connection settings, or response parsing; Spring Boot handles all these concerns behind the scenes.

### LoadBalancer
Suppose there's too much of load to address-service and it can't handle all the incoming requests. We can scale up address-service so that requests can be routed to different instances of the service.
Also, remember that we have hardcoded the url in FeignClient for the service(address-aservice).

<img width="1071" alt="Screenshot 2024-07-12 at 3 04 18 PM" src="https://github.com/user-attachments/assets/1ec4e018-f752-4d67-ab7d-0ea1d3125115">

#### How the load should be equally distributed though (in cases when there are multiple service instances )(consider address-service instances)?

<img width="527" alt="Screenshot 2024-07-12 at 2 59 27 PM" src="https://github.com/user-attachments/assets/296a6710-d2ca-4554-a653-32f4cd1dc7a2">
<img width="512" alt="Screenshot 2024-07-12 at 2 58 34 PM" src="https://github.com/user-attachments/assets/bdc754b9-787f-4de1-82de-9174463c6c50">

We can have a Loadbalancer that can help in routing calls/requests to address-service from employee-service.

<img width="1100" alt="Screenshot 2024-07-12 at 3 03 46 PM" src="https://github.com/user-attachments/assets/b4b54c1d-7378-4237-becf-3eb55167bc89">
<img width="1100" alt="Screenshot 2024-07-12 at 3 03 46 PM" src="https://github.com/user-attachments/assets/7d6cd987-fc56-47b6-a1fe-5464e5f96ed2">

The configured Loadbalancer can route requests to multiple servers.

<img width="1071" alt="Screenshot 2024-07-12 at 3 04 18 PM" src="https://github.com/user-attachments/assets/04bc7777-1515-419e-97bd-fa08c404f090">

If we remove URL, we need to define Loadbalancer for FiegnClient.

<img width="1093" alt="Screenshot 2024-07-12 at 3 08 42 PM" src="https://github.com/user-attachments/assets/d90c727b-6928-4f1f-8e61-45ad27dc62dd">

## Ribbon

We have a client-side Loadbalancer called Ribbon.

Older versions of Spring cloud had Ribbon support. We can use Hoxton versions.

<img width="590" alt="Screenshot 2024-07-12 at 3 15 03 PM" src="https://github.com/user-attachments/assets/799e92f7-afbd-4963-928b-beb55bf26d76">

Downgrade spring-parent version

<img width="604" alt="Screenshot 2024-07-12 at 3 16 21 PM" src="https://github.com/user-attachments/assets/4a255692-5aec-449e-9d79-fce54a58ba55">
<img width="672" alt="Screenshot 2024-07-12 at 3 17 41 PM" src="https://github.com/user-attachments/assets/8f7a0e91-87c2-41dd-86d3-dc04c9dd7386">

Add RibbonClient

<img width="637" alt="Screenshot 2024-07-12 at 3 19 41 PM" src="https://github.com/user-attachments/assets/c3a53b0c-7eea-4ddf-849e-3c50d6a55180">
<img width="829" alt="Screenshot 2024-07-12 at 3 19 08 PM" src="https://github.com/user-attachments/assets/c6af8818-3d6b-4168-adda-8e7b59fa5fe9">

Run the application & we'll be able to see which server is the request routed to by Loadbalancer.

<img width="849" alt="Screenshot 2024-07-12 at 3 23 30 PM" src="https://github.com/user-attachments/assets/02616aca-01ba-4461-a928-72e1374bedf7">

Sometimes it is routed to 8081 and sometimes to 8082.

<img width="744" alt="Screenshot 2024-07-12 at 3 25 13 PM" src="https://github.com/user-attachments/assets/ebf157b6-bd70-46ea-8e8a-de47920e2378">

### Understanding the pattern

Round Robin Fashion- sequentially distribute the routing. We can change the logic as well.




