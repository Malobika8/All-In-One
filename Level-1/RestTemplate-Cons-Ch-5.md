*RESTTemplate is a part of the Spring Framework in Java, used for making HTTP requests and sending HTTP messages to the RESTful web services. It provides methods for GET, POST, PUT,
DELETE, and other requests. The RESTTemplate allows you to make a request to a URL and retrieve the response in a convenient way. It also supports various features such as URL
encoding, JSON serialization, and error handling. By using the RESTTemplate, you can write concise and readable code for interacting with RESTful web services. It simplifies the
process of making HTTP requests in your Java application.*

## Why should we avoid using RestTemplate?

*Blocking Calls — RestTemplate
This thread waits for the response before moving on to other tasks. However, this approach can lead to problems when dealing with many requests, especially if some of them are waiting
for slow services to respond.*

*RestTemplate is a convenient way to make HTTP requests in Spring-based applications, but there are some reasons to avoid using it. Firstly, it's not thread-safe, which can lead to
issues in multi-threaded environments. Secondly, it's quite rigid and doesn't allow for advanced HTTP feature customization, such as connection pooling and caching. Additionally, it
doesn't handle errors and exceptions well, which can make debugging challenging. Finally, it's considered a low-level API, and newer alternatives like WebClient and Feign offer more
flexibility and better performance. Therefore, it's recommended to use more advanced and flexible HTTP clients for complex use cases.*

### Note:
*RestTemplate isn't deprecated yet but will be in a future update. The Spring team recommends using WebClient, as RestTemplate won't receive new features.
In Spring 5.x, a new WebClient API was introduced, which provides better support for asynchronous and non-blocking web requests. While RestTemplate is still available, WebClient is 
considered the recommended alternative for new applications.*

### How Request is processed?

When a request is sent from the client to the server, it triggers a thread in the server's process. In a request-response model, a new thread is created for each incoming request, 
allowing multiple clients to be served concurrently. The server's operating system allocates a new thread from the thread pool, and the thread is responsible for processing the 
request. The thread executes the server's application code, retrieves the requested data, and sends the response back to the client. This process is known as a "thread-per-request" 
model, where each request is handled by a dedicated thread.  

<img width="1093" alt="Screenshot 2024-07-12 at 10 27 13 AM" src="https://github.com/user-attachments/assets/8ec108f0-22fb-43e6-92eb-124964627c03">

Considering Tomcat: 
- Inside Tomcat Server, App is deployed.
- Client makes Server call.
- Server has thread pool.
- These threads help a client to process a request.
- Threads take the responsibility to capture & process Requests.
- Once Response is sent back to the client, the thread is deallocated and becomes ready to take another Request.

*Limitation: Server has a bunch of threads but it is limited.*

Imagine a scenario where there is a Database. There is one Client hitting a request and say Thread-1 processes the same. Now,the thread remains ideal till the Database processes and sends 
back the result. Once this is done, Thread-1 gives the response back and then finally deallocated.

Now, Instead of a database we can even think of a Restful Application.

Suppose there's a new request, & Thread-2 is responsible to process the request and connect to the Rest API. However, it sits ideal till it gets the response. Once it gets the response,
it sends it back to the Client. So it basically stays ideal for a considerable period of time.

Now imagine there are multiple Concurrent Requests coming in which is greater than the number of Threads available. The threads will process the request and sit ideal till they get back the response.

#### What if, in between, another Client sends a Request?

Since there isn't any thread available to take up the request, there will be huge lag in application (we won't get the response back).

This is why whenever we pay to a Vendor we look for good Servers. 

```
Example: Server1 capabilities - 1gb, 2 core, 40 threads. 

What if 41 concurrent calls are made? - It will be unresponsive.
```

### Why can't we scale up the Servers? Why can't we have multiple instances of the Service? (with load balancer)

- This is extremely cost heavy & internally all of this uses same synchronous call.

RestTemplate is a blocking call. The moment it executes, it doesn't go to the next line as the thread gets blocked till the Request is processed and Reponse is given back. 

Till that time, the Thread remains ideal.

<img width="833" alt="Screenshot 2024-07-12 at 10 43 36 AM" src="https://github.com/user-attachments/assets/8bea4caa-a8a2-41d5-b865-4efef491ddbd">

In our case the DB call and external Rest API call are both blocking calls.

<img width="864" alt="Screenshot 2024-07-12 at 10 45 43 AM" src="https://github.com/user-attachments/assets/6a494d9b-09a1-4d70-b9b6-8f6b6324baee">

## FYI

To convert to reactive spring project.

<img width="956" alt="Screenshot 2024-07-12 at 10 49 02 AM" src="https://github.com/user-attachments/assets/49619c12-875e-42f2-bc07-cdded944b563">
<img width="581" alt="Screenshot 2024-07-12 at 10 50 06 AM" src="https://github.com/user-attachments/assets/6c6b888b-97e7-4ddd-98bd-61e3a5bf71f4">
<img width="809" alt="Screenshot 2024-07-12 at 10 50 43 AM" src="https://github.com/user-attachments/assets/43d5cd41-7698-47a1-89b9-009867b19001">

Our application will now support reactive programming.

We can make reactive/asynchronous call. We can reuse our Threads.

Sample:

<img width="858" alt="Screenshot 2024-07-12 at 11 00 06 AM" src="https://github.com/user-attachments/assets/5dea076c-770b-486e-bd53-72f711cf15f8">
<img width="1009" alt="Screenshot 2024-07-12 at 10 59 24 AM" src="https://github.com/user-attachments/assets/e6ab89d3-f052-4c09-9658-24c4d22b2c97">

### Q. Difference between a blocking call and non-blocking call?

