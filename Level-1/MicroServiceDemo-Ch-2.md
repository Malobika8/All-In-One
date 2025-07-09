# What are microservices?

Microservices - also known as microservice architecture - is an architectural style that structures an application as a collection of services that are:
- Independently deployable
- Loosely coupled. Services are typically organized around business capabilities. Each service is often owned by a single, small team.
- Microservices is an approach using what we can develop small services 
- Each service should run on its own container/server/process.
- The services should be lightweight

# Why Spring? Why should we use a Spring Framework?

- Fast Development
- Less Configuration
- AutoConfiguration
- Embedded server
- Production Ready
- Starter Projects
- Readymade support for Microservices through Spring Cloud
  
# SpringBoot to develop Microservices?

- AutoConfiguration
- Loose coupling
- Managed dependencies
- Support load balancer
- Open source

### Create a simple address-service Application & employee-service Application
- Dependencies required:

  <img width="871" alt="Screenshot 2024-07-10 at 9 28 42 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/db1791dd-195f-4d92-850d-75d20fc50218">

- *address-service Application*

  <img width="1034" alt="Screenshot 2024-07-10 at 9 12 09 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b7aa5c8d-007d-4dab-b4eb-bf50d7ffd961">

  This runs on port 8080

  <img width="886" alt="Screenshot 2024-07-10 at 9 13 07 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/eacb6a1a-f83e-40b6-b865-656a381516aa">

- *employee-service Application*

  <img width="1027" alt="Screenshot 2024-07-10 at 9 11 59 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/45e66d2d-e965-45d8-aeab-d70fe0c0e957">

  This run on port 8081

  <img width="950" alt="Screenshot 2024-07-10 at 9 13 15 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/1143767c-fae1-4455-aad3-a27625eb62e1">

**Let's see how our microservices can talk to each other.**

Requirement: We need to show address data along with employee data.

We would need address data(through Rest call) from address service and it can be concatenated with employees details in employee service.

For Rest calls using SpringBoot, we need a RestClient. In our case, we'll Rest Template.

### FYI
```
RestTemplate is deprecated and might be removed from spring 6.X.

Going forward, we will use Feign Client, Webclient as it's replacement.
```

<img width="1022" alt="Screenshot 2024-07-10 at 9 18 40 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/83a38a69-9740-4dfa-94fd-748169dd89ad">
<img width="1028" alt="Screenshot 2024-07-10 at 9 25 05 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d12d4cc7-85c1-45dc-9c62-749e62371cfc">

When we run employee-service, it fails to start as it complains of unavailability of Rest Template bean.

<img width="1331" alt="Screenshot 2024-07-10 at 9 23 44 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2815cb30-b884-40c8-a21d-481f32ddc61b">

#### Create a Rest Template bean

<img width="1440" alt="Screenshot 2024-07-10 at 9 27 00 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/6ceb0109-4264-41aa-8384-e4c97ffb48d4">

#### Run the Application

<img width="1242" alt="Screenshot 2024-07-10 at 9 27 14 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/4a778daf-b5d1-4e7d-857e-ca93073949f5">




