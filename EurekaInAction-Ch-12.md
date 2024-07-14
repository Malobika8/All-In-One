## Continuation

Both of our Services are up.

<img width="1114" alt="Screenshot 2024-07-14 at 1 02 00 PM" src="https://github.com/user-attachments/assets/782dcc4a-6848-4814-96a9-92be03ba7839">

Currently, we have the *address-service* URL (port and hostname) hardcoded in application.properties.

<img width="744" alt="Screenshot 2024-07-14 at 1 07 46 PM" src="https://github.com/user-attachments/assets/b8b0915d-2ee9-40f4-8da9-29d524aa8b5b">

This is not a good approach. 

*(What if it runs on a different port?)*

Let's suppose we are using *RestTemplate*.

<img width="1110" alt="Screenshot 2024-07-14 at 1 12 16 PM" src="https://github.com/user-attachments/assets/5b9e7c97-9398-43a6-ac03-64f3cf27158d">

We don't want to Hardcode the IP & port number.

<img width="1070" alt="Screenshot 2024-07-14 at 1 15 20 PM" src="https://github.com/user-attachments/assets/51158637-0b57-404c-a5a5-7783ac93a509">

## How to not Hardcode the URI?

We need Discovery Service to get us the details(IP and port number) of *address-service*. Currently, we have only one instance of *address-service* running. Hence, we tried to get the 
one present in the "0th" index.

<img width="1104" alt="Screenshot 2024-07-14 at 2 19 06 PM" src="https://github.com/user-attachments/assets/c96a297c-503e-4ffd-bf84-12636278a946">

*ServiceId* is nothing but the application name that we have set.

<img width="746" alt="Screenshot 2024-07-14 at 1 18 29 PM" src="https://github.com/user-attachments/assets/7c185f6e-7636-46f9-863e-ccbd852e5c95">

*ServiceInstance* contains all the information.

<img width="1103" alt="Screenshot 2024-07-14 at 1 20 22 PM" src="https://github.com/user-attachments/assets/f0c68e05-87cf-413f-bef4-d43fa6e0ff81">

Run *emp-service* and it should work fine. We can print the URI and check that it is picking up the URI correctly.

<img width="685" alt="Screenshot 2024-07-14 at 1 22 33 PM" src="https://github.com/user-attachments/assets/8e851074-a6d9-47bd-840e-5fd53e3472af">

Let's now stop the instance and start again on a new port.

<img width="807" alt="Screenshot 2024-07-14 at 1 28 10 PM" src="https://github.com/user-attachments/assets/e50c5ba8-57a7-4539-b8f2-3c6f64563230">

A few seconds later, we would see the changes being reflected.

```
It tries with the address-service URI few times before trying to check Discovery Service for updates and availability of new address-service instances. Once it gets the same,
it hits the new instance URI.
```

<img width="810" alt="Screenshot 2024-07-14 at 1 29 29 PM" src="https://github.com/user-attachments/assets/50d4d523-da93-49bf-9289-de7f6a546e1b">

Note that we are currently not load-balancing. We are only fetching the instance present in the 0th position.

# Spring Cloud Load Balancer

We can use LoadbalancerClient instead of DiscoveryClient.

<img width="1036" alt="Screenshot 2024-07-14 at 2 05 48 PM" src="https://github.com/user-attachments/assets/e0f7c49f-ba53-45f6-b6bf-432b35aa4e90">

Now, if we try to hit the address-service endpoint, we would notice it calls different address-service instances every time. 

(Default - sequential manner(Round Robbin))

<img width="938" alt="Screenshot 2024-07-14 at 2 06 41 PM" src="https://github.com/user-attachments/assets/333b8b47-aa87-452c-9f03-567bfadbf3f6">
<img width="933" alt="Screenshot 2024-07-14 at 2 06 50 PM" src="https://github.com/user-attachments/assets/06422777-64f1-41a4-9bf6-4cb1fee7bd20">

We can print the URI in *employee-service* and confirm the same.

<img width="905" alt="Screenshot 2024-07-14 at 2 08 51 PM" src="https://github.com/user-attachments/assets/67e55683-a635-4a5e-9390-411bb176d625">

The context path of *address-service* should be dynamic as well.

We can have properties that are shareable and are necessary for other applications. So, in *address-service*, we can add,

<img width="859" alt="Screenshot 2024-07-14 at 2 14 43 PM" src="https://github.com/user-attachments/assets/be0c67ff-81e4-4647-89b8-d4cc9f6edd48">

Metadata is a Map.

<img width="813" alt="Screenshot 2024-07-14 at 2 14 08 PM" src="https://github.com/user-attachments/assets/4605208d-0027-4d0d-a41d-70255f619dbc">
<img width="978" alt="Screenshot 2024-07-14 at 2 16 44 PM" src="https://github.com/user-attachments/assets/30a1cc72-09ab-4334-80ca-cda05e07495f">

# Magic

Any of what we discussed is not required. We can directly ask Eureka to provide us with the details related to the ServiceId provided using *RestTemplate*.
Our RestTemplate connects with Eureka and gets the context-path/other details with the service ID provided. SeviceId is nothing but the service name that has been set. 
Eureka gets the list of instances from which any one is chosen.

<img width="793" alt="Screenshot 2024-07-14 at 2 43 07 PM" src="https://github.com/user-attachments/assets/cb6f5d07-b461-41a2-986b-db8133281c6d">

But we would come across "UnknownHostException".

<img width="891" alt="Screenshot 2024-07-14 at 2 35 47 PM" src="https://github.com/user-attachments/assets/2c4640f2-3964-4010-9a8d-e993b004166a">

### Also, who would do LoadBalancing?

We need to ask RestTemplate to do load balancing for us. This will do all the internal stuff that we did previously.

<img width="1087" alt="Screenshot 2024-07-14 at 2 38 00 PM" src="https://github.com/user-attachments/assets/aaaa2fe9-8472-4362-8372-d70edbe1b3e4">
<img width="1067" alt="Screenshot 2024-07-14 at 2 46 59 PM" src="https://github.com/user-attachments/assets/4a2766bf-2460-4731-8724-8afefa80a6f9">

Our application uses "Spring-cloud" load balancer.

## Disadvantage of Client-side load balancer

- every client will have a load balancer which would make things complicated and bulky.

In the case of server-side load balancing, there will only be one to handle all these.

<img width="1227" alt="Screenshot 2024-07-14 at 2 51 53 PM" src="https://github.com/user-attachments/assets/b56184be-3ef3-487b-9041-3a1612a18ef6">
<img width="1270" alt="Screenshot 2024-07-14 at 2 51 13 PM" src="https://github.com/user-attachments/assets/e2850a2a-956d-4081-8609-e92fd968da33">





