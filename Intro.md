# Web Services 
### (A service that's made available with the web)

A web service is a set of open protocols and standards that allow data to be exchanged between different applications or systems. It is a software system that provides a specific 
functionality or service to other applications over the web. It enables communication between different systems, allowing them to exchange data and functionality. Web services are 
typically implemented as a RESTful API, which uses HTTP requests and responses to interact with clients. They can be built using various programming languages and frameworks, and can 
be deployed on multiple platforms. Examples of web services include payment gateways, social media APIs, and weather services, which provide data and functionality to other applications
and users.  

### Isn't everything online (Ecom, Chatting apps etc) is a WebService then? 

The difference between a standard Website and a WebService is that a Website is meant for Human consumption while a WebService is meant for Code consumption or Application-level consumption.
A WebService allows 2 different machines / 2 different pieces of code / 2 different applications running on 2 different servers to be able to talk to each other.

## Types

There are primarily 2 different type:
1) *SOAP (Older) (Simple Object Access Protocol):*
   
   - This works upon HTTP client.

     Suppose there's Client and a Server and they interact with the help of SOAP API.
     Now the different parameters we have to consider are:
    
     1) Endpoint URL: We would need this whenever we are sending any request
     2) Data format: Requests would always be sent in the form of xml
     3) Response: Response received in the form of xml as well as Response code (success status)

   - SOAP is not preferred these days. Consider a scenario where we are sending a Form with multiple fields. Web Page would convert it into       single XML file and then send the same to 
     Server. Server would then read data one by one and insert into the Database. Bounded to XML can be considered as a limitation as             request can be sent only in the form of XML.
     Moreover, XML is complex and sometimes not lightweight.

   - XML was once considered one of the best communication medium between two Systems. But there are new Technologies nowadays which is why       SOAP is almost gone.
   - SOAP also doesn't have any Header facility.
  
     <img width="265" alt="Screenshot 2024-06-22 at 9 44 22 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/e8b74b2d-f78c-4ed0-998b-eb9f4ddce38d">

3) *REST (Representational Stateful API's):*
   
   - Works on HTTP.

     The different parameters we have to consider are:
     
      1) Endpoint URL: We would need this whenever we are sending any request.
      2) Data Format: Need to pass Data. Unlike SOAP, in case of REST, different types of content are supported - XML, JSON, String, Doc              etc. We can send request in any format. These are called MIME Type. This is the biggest advantage over SOAP. 
      3) Diff types of operations can be performed with REST API's (CRUD).  
      4) We need to pass Headers which basically contains info related to the Content Type that is passed (JSON/XML etc). It also includes            Username or Password for Authentication.
      5) Response: This can again be of any Type (JSON, XML, String etc).  We get Response in the form of Response Code (200..204..400.404            etc).

         <img width="375" alt="Screenshot 2024-06-22 at 9 59 59 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ec60a842-db8f-4aaa-ba45-cdb1d43e7112">

## In the Java world, there are 2 different specifications.
- There's a specification for SOAP WebServices called JAX-WS
- There's a specification for REST WebServices called JAX-RS

## Tools available for SOAP and REST (for Manual and Automation Testing of WebServices)

1) SOAP UI - Supports both SOAP and REST 
2) POSTMAN - Supports only REST
3) Rest Client / Advamced Rest Client - Supports only REST
4) HTTP Cient - Supports only REST
5) Rest Assured - Supports only REST
6) Jersey Client - Supports only REST
7) SOAP Client - Supports only SOAP
8) JMeter - Supports only REST

## Check out 

https://reqres.in/
