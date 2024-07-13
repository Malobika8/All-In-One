# Service Discovery

For one service to hit the endpoint of another service, we require two things:
- Server IP
- Server Port

But it may be dynamic.

#### How would we discover the service then?

<img width="946" alt="Screenshot 2024-07-13 at 6 44 06 AM" src="https://github.com/user-attachments/assets/e9fe7fa0-c776-41f6-b0fe-d1c987939006">

In a Monolithic Architecture, the service calls will be local and not remote since they are zipped as one war and deployed on the same server. There isn't going to be any time/network 
latency.

<img width="975" alt="Screenshot 2024-07-13 at 6 45 28 AM" src="https://github.com/user-attachments/assets/e34edc2b-e539-4bfa-808e-3e8a4107c80d">

This is not the same for distributed systems (Microservices Architecture). The service calls will be remote. There will be time latency.

<img width="1009" alt="Screenshot 2024-07-13 at 6 48 59 AM" src="https://github.com/user-attachments/assets/3c89f7e6-e8bd-4ddd-8ed5-4de8329ea031">

Suppose Service "B" is deployed to a server with port number and IP. Now, Service "A" wants to hit an endpoint, we need the Service "B" URL.

<img width="1149" alt="Screenshot 2024-07-13 at 6 51 28 AM" src="https://github.com/user-attachments/assets/f6064774-2dde-4073-acc0-821d8501c5e9">

Suppose now the load increases and Service "B" needs to be scaled up as Servers has limitations on the number of requests it can handle because of a limited number of threads.

Since there will be multiple URLs, it is not feasible to note all of them. Some of them might be dynamically changing with Server restart. Also, the servers might be scaled up and down
based on the load. So some of the servers might not even exist anymore.

<img width="1259" alt="pic2" src="https://github.com/user-attachments/assets/72390488-061c-4188-a542-c6e159b20156">

We need to find a way to be able to dynamically discover the service instances.

### Traditional Load Balancing

All the services are registered with the LoadBalancer and it knows all the details(IP, port) related to the same. On the other hand, Loadbalancer has a URL of its own. When Service "A" 
wants to hit a Service "B" endpoint, it won't directly call the Service "B" url but Loadbalancer which will then route the request forward to service instances.

<img width="1217" alt="Screenshot 2024-07-13 at 7 00 22 AM" src="https://github.com/user-attachments/assets/80772d8a-50b8-46f0-a22a-0fb6a2f236dd">

This is called *Server-side* load balancing since Service "A" doesn't call Service "B" directly. It calls the Loadbalancer(Router Server) instead.

### Why can't it be used with MicroServices?
- One remote call converted to two remote calls
- Single point of failure (If LoadBalancer fails, the entire system fails)
- Need maintenance cost and a separate team to handle LoadBalancer
- Need manual configuration
- Does not support scalability
- Not Container friendly as it cannot be scaled up and down

## Discovery Service - Server Side Discovery

MicroServices registers with Discovery Service. Discovery Service, int turn, gets to know the IP, port, and other details of every Service (Service "A" and "B").
The service instances register themselves with DiscoveryService. In turn, it maintains the list.

With every request, LoadBalancer queries with the DiscoveryService. It gets to know the service instances list and then routes to one of the instances.

<img width="1220" alt="Screenshot 2024-07-13 at 7 18 43 AM" src="https://github.com/user-attachments/assets/4c8b8548-1976-4e24-86fd-a5ab5fa9a3f2">

- The LoadBalancer maintains the load
- It exists inside a different Server
- Service "A" makes a request to a Server/Router/LoadBalancer
- LoadBalancer queries the Discovery Service and routes the request to one of the available Service instances

<img width="1242" alt="Screenshot 2024-07-13 at 7 19 27 AM" src="https://github.com/user-attachments/assets/3ea03008-a30a-40b5-bb04-baac48c6d86f">

## Client Side Discovery

<img width="1183" alt="Screenshot 2024-07-13 at 7 22 27 AM" src="https://github.com/user-attachments/assets/3d5853ff-18f1-4e0a-aa67-d2989660cb5c">

The client asks for website info from the directory and calls the website directly. 

- Services register themselves with Service Discovery
- Service "A" queries the Discovery Service and gets the service instance details
- It then directly makes a call to one of the service instances.
- There is no LoadBalancer in this case. The client itself does the load balancing.

<img width="1187" alt="Screenshot 2024-07-13 at 7 26 32 AM" src="https://github.com/user-attachments/assets/e628f5d0-b74e-444e-b9a2-40fcc995e43c">
<img width="1165" alt="Screenshot 2024-07-13 at 7 26 40 AM" src="https://github.com/user-attachments/assets/9db405b1-7543-4b28-a5bf-32612f0ec4c2">

Still, there are 2 different network calls. One to the discovery service and the other to one of the Service instances.

However, next time it wants to hit service "B", since the list retrieved from Discovery service is cached in data, it doesn't need to look up and query the discovery service again.

<img width="1191" alt="Screenshot 2024-07-13 at 7 46 46 AM" src="https://github.com/user-attachments/assets/7216d6c0-4336-49b2-ae6e-0e9d24033dd6">

### Can we still improve it?

Services register with Discovery Services and cache the entire registry so that it doesn't have to query again and again for different service calls.

<img width="1243" alt="Screenshot 2024-07-13 at 7 32 51 AM" src="https://github.com/user-attachments/assets/8174db15-4ec8-4ed3-9e25-4e113110cbbf">
<img width="1215" alt="Screenshot 2024-07-13 at 7 33 48 AM" src="https://github.com/user-attachments/assets/47aaba52-ac0e-4d07-ab85-560291458ac3">

#### What if an instance goes down?

<img width="1222" alt="Screenshot 2024-07-13 at 7 37 03 AM" src="https://github.com/user-attachments/assets/c0879d2a-e743-4243-802c-d77ca29cd198">
<img width="1270" alt="Screenshot 2024-07-13 at 7 36 47 AM" src="https://github.com/user-attachments/assets/bf5a6815-e7ca-4757-af18-ae7f6b528e1c">

## Libraries to implement Client and Server Side Discovery

- Client Side Service Discovery
  - Netflix Eureka
  - Apache Zookeeper
  - Consul
- Server Side Service Discovery
  - NGINX
  - AWS ELB

### FYI

<img width="1153" alt="Screenshot 2024-07-13 at 7 43 34 AM" src="https://github.com/user-attachments/assets/c8d52572-7dfe-4dcb-b8ad-3bc7217d5030">


