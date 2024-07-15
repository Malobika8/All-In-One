### Why do we need an actuator in SpringBoot?

- For service Health Check
- Monitor different things related to our MicroService

Currently, it is not showing anything since we don't have any actuator implementation.

<img width="677" alt="Screenshot 2024-07-15 at 12 10 13 PM" src="https://github.com/user-attachments/assets/d6b9622e-7a59-4a82-9291-a68997eb47f8">

We can implement Actuator.

- Add SpringBoot actuator dependency

  ```
  <!-- https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-actuator -->
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-actuator</artifactId>
      <version>3.3.1</version>
    </dependency>
  ```
  Run the application. The health endpoint comes free and should work just fine.

  <img width="759" alt="Screenshot 2024-07-15 at 12 15 34 PM" src="https://github.com/user-attachments/assets/6a67a497-e7e6-4abc-86b7-39274c1d19d0">

- Activate info endpoint: We need to add a property.

  ```
  management.endpoints.web.exposure.include=*
  ```

  <img width="1150" alt="Screenshot 2024-07-15 at 12 17 56 PM" src="https://github.com/user-attachments/assets/397b1d85-7de4-45bc-868f-ac72af1a6492">
  <img width="700" alt="Screenshot 2024-07-15 at 12 20 28 PM" src="https://github.com/user-attachments/assets/7fc00cff-9e89-4609-ba36-8f3bfe33f954">
  <img width="815" alt="Screenshot 2024-07-15 at 12 19 16 PM" src="https://github.com/user-attachments/assets/be43bdfe-b5b9-4773-910b-1cc4cbb92e82">
  <img width="845" alt="Screenshot 2024-07-15 at 12 20 44 PM" src="https://github.com/user-attachments/assets/a3652586-c64e-4f93-87e7-47bf686b5ba9">

# Eureka + Feign Integration

Rest Client calls using OpenFeign. 

*Note: OpenFeign does load balancing automatically.*

<img width="900" alt="Screenshot 2024-07-15 at 12 49 15 PM" src="https://github.com/user-attachments/assets/fbd13677-527d-4fc2-90b0-5d433acfc39e">

If we don't use Eureka, we must manually add the spring load balancer.

<img width="882" alt="Screenshot 2024-07-15 at 12 49 43 PM" src="https://github.com/user-attachments/assets/1ef2873e-e15a-4511-9ac3-7db75efc7aa7">
<img width="782" alt="Screenshot 2024-07-15 at 12 49 57 PM" src="https://github.com/user-attachments/assets/7e877d24-a87c-4a32-9139-7ec76d1818d6">

- Required Dependency:

  ```
  <!-- https://mvnrepository.com/artifact/org.springframework.cloud/spring-cloud-starter-openfeign -->
    <dependency>
      <groupId>org.springframework.cloud</groupId>
      <artifactId>spring-cloud-starter-openfeign</artifactId>
      <version>4.1.2</version>
    </dependency>
  ```
- Create an Interface for FeignClient

  It would do load balancing as well. Eureka Instance name would get us the URI.
  
  <img width="986" alt="Screenshot 2024-07-15 at 12 43 18 PM" src="https://github.com/user-attachments/assets/ead9a02b-2891-48b3-8004-93bc40733daf">
  <img width="1091" alt="Screenshot 2024-07-15 at 12 45 42 PM" src="https://github.com/user-attachments/assets/6b97f203-a638-4acc-a73a-4d62a6afd03c">

  Use it in the Controller

  <img width="1093" alt="Screenshot 2024-07-15 at 12 38 41 PM" src="https://github.com/user-attachments/assets/0df858d7-d2ce-4534-96b9-bc5a5b0c39c6">

  #### Note: Loadbalancing is done by **default** in *RoundRobin* fashion. 

### Setting up a Custom Load Balancer

<img width="715" alt="Screenshot 2024-07-15 at 12 56 43 PM" src="https://github.com/user-attachments/assets/edc139d5-cdb0-4249-81ec-961fc7a929c7">
<img width="951" alt="Screenshot 2024-07-15 at 12 57 27 PM" src="https://github.com/user-attachments/assets/1302cf56-6557-4cdf-b747-d05119bc921a">
<img width="936" alt="Screenshot 2024-07-15 at 12 59 48 PM" src="https://github.com/user-attachments/assets/4c16f469-55cb-4e9b-9ff1-b8507620de10">
<img width="893" alt="Screenshot 2024-07-15 at 1 03 13 PM" src="https://github.com/user-attachments/assets/cd973a1e-c334-4fd8-867a-581f5ee5675c">
<img width="913" alt="Screenshot 2024-07-15 at 1 00 44 PM" src="https://github.com/user-attachments/assets/437b3195-7346-4d25-a2d9-14990afa8931">

## Database Architecture

Our Database Architecture currently,

<img width="1056" alt="Screenshot 2024-07-15 at 1 07 06 PM" src="https://github.com/user-attachments/assets/a66f1e61-9b03-4a13-b622-f8405d15c10b">

We shouldn't be doing this. Every MicroService should have its own Database.

<img width="1102" alt="Screenshot 2024-07-15 at 1 11 15 PM" src="https://github.com/user-attachments/assets/14e8eeaa-98c1-4aaf-8e6e-d68b6bd96af9">




  

  
