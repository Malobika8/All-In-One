### Let's recall

<img width="1132" alt="pic1" src="https://github.com/user-attachments/assets/af0f11e8-21f2-4b69-8bc6-71902f2552eb">
<img width="1076" alt="pic2" src="https://github.com/user-attachments/assets/2056380c-5956-4fd5-8c1f-15968d82bd07">
<img width="1054" alt="ic3" src="https://github.com/user-attachments/assets/09380759-fe7f-40c8-b8b9-693fae409500">

*Note: Port no 0 : Dynamically allocates a port number*

# Things we should know before proceeding further

Consider a scenario where multiple services are deployed. 

### But where exactly are the Services deployed?

We need to take them to Data Centre (a place where we have big Servers and can put our Services).

```
A data centre is a facility used to house computer systems and associated components, such as servers, storage systems, and networking equipment. These
facilities serve as primary locations where data is processed, stored, and distributed to various stakeholders. Data centres are responsible for managing and maintaining vast amounts
of digital information, providing scalable and reliable computing resources to organizations. They play a crucial role in powering online services, cloud computing, and big data
analytics, ensuring efficient data processing and storage for businesses and individuals worldwide.
```

### What if the Data Centre gets destroyed?

We have multiple Data Centre's in a location for backup.

<img width="730" alt="Screenshot 2024-07-13 at 9 37 23 AM" src="https://github.com/user-attachments/assets/ee886a6b-36f8-4903-8e33-18d87607d22e">

There are regions and zones.

<img width="1225" alt="Screenshot 2024-07-13 at 9 38 54 AM" src="https://github.com/user-attachments/assets/9ccf7c6c-8c98-4234-b537-e39f45334f70">

Different regions for AWS

<img width="931" alt="Screenshot 2024-07-13 at 9 39 30 AM" src="https://github.com/user-attachments/assets/712ee14c-22f3-4a90-8a1b-aa548ae61dd0">
<img width="539" alt="Screenshot 2024-07-13 at 9 41 10 AM" src="https://github.com/user-attachments/assets/63221eb8-0841-45ac-a381-8a686c5ce2e8">

*Note: The exact location of the Data Centre is kept private for obvious reasons.*
*Note: Cross regions calls have a lot of latency and hence are avoided.*

So, our microservices are deployed in different zones of regions. Cross zone latency is comparatively less.

<img width="1209" alt="Screenshot 2024-07-13 at 9 46 53 AM" src="https://github.com/user-attachments/assets/42838f6f-fea4-4a84-a08d-e6d13e3b2e3a">

#### What if we have 1 Discovery Service for all the zones of a region?

<img width="1227" alt="Screenshot 2024-07-13 at 9 49 31 AM" src="https://github.com/user-attachments/assets/afeba032-0cfb-41b1-b877-c45a2b1327ae">
<img width="1225" alt="Screenshot 2024-07-13 at 9 58 47 AM" src="https://github.com/user-attachments/assets/36598332-fbd0-48da-ba04-ccf478c88b9a">

- If the DS fails, everything will collapse.
- Also, if DS is in one zone, for other zones to connect to the DS, it will be a cross zone connection which might again lead to time latency.

Rather, different Eureka Discovery Services are maintained for different zones (in a Region). All these eureka servers communicate with each other and sync. Any new data captured by Eureka Service is 
shared with others (It spreads like Infection).

*Note: DS doesn't communicate with another DS present in a different Region.*

<img width="1227" alt="Screenshot 2024-07-13 at 10 00 08 AM" src="https://github.com/user-attachments/assets/fbd844b1-1ff4-4b9a-8431-35b71312180e">

We need to have a Discovery Service and inside this, we need to register the services.
