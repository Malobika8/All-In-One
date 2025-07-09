# Microservices Communication

### Objective: emp-service should get us address details as well when we hit the employee endpoint.

<img width="1196" alt="Screenshot 2024-07-11 at 8 18 01 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/43f0daa0-f0bc-4865-84a1-9376eac8cec2">

It's a good practice to set Context Path.

<img width="1042" alt="Screenshot 2024-07-11 at 11 05 20 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9a544b9f-cc0a-41fb-840e-73bc90dac147">

Since we want to get the address details of the employee when we hit the employee endpoint, we can add *AddressResponse* in *EmployeeResponse*.

<img width="1063" alt="Screenshot 2024-07-11 at 10 24 38 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/82a896e2-24c5-4df2-a5af-9ae4c76bf56f">

### To make REST calls, we can use Rest Template.

The address details of the employee are added to *EmployeeResponse*.

```
*Note: From Spring 5 RestTemplate is deprecated and no autoconfiguration is provided. Hence, we need to create a bean for it manually.*
```
<img width="1060" alt="Screenshot 2024-07-11 at 10 30 28 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/06f9e98a-b6de-4b35-a504-bcd631b6f2ef">

It is a good practice to retrieve elements such as the baseUrl from a properties file rather than hardcoding it directly into the code.

<img width="984" alt="Screenshot 2024-07-11 at 10 27 04 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b795ea74-fbb9-4544-a1e7-54660c2a3211">
<img width="1386" alt="Screenshot 2024-07-11 at 10 26 23 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9b4f3a2d-046a-43cb-a3f2-d0f6abb2f91e">

Run the Application & we should get all the details related to the employee including address details.

<img width="1407" alt="Screenshot 2024-07-11 at 10 31 23 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c2d0b37b-9a40-4037-b7fa-2127fec5f861">

*employee-service communicates with address-service to get all the address details of the related employee and shows the same.*

#### This is a very good example of MicroServices communication. 

# FYI

Another way to create RestTemplate object

<img width="743" alt="Screenshot 2024-07-11 at 10 38 12 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a589dcb6-4194-4b30-b4c3-1d0ac9076229">
<img width="673" alt="Screenshot 2024-07-11 at 10 37 54 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/0b9ef414-8546-4397-9502-b8172800fffd">

We can also add our addressBaseUrl in the same.

<img width="1007" alt="Screenshot 2024-07-11 at 10 39 42 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/18affaf1-ee09-4842-8e75-0ce559c0a910">

We need to add it as Constructor parameter otherwise it will be null as value is set after Bean creation.
<img width="978" alt="Screenshot 2024-07-11 at 10 42 12 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/61a235aa-06e9-47d9-bb88-a47dfd673574">
<img width="1056" alt="Screenshot 2024-07-11 at 10 43 14 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/1909e347-2a95-490c-9adc-45e49457be12">







