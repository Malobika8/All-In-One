# Intro

### OpenAPI3 & SpringBoot official Documentation - https://springdoc.org/

<img width="984" alt="Screenshot 2024-07-27 at 8 39 19 PM" src="https://github.com/user-attachments/assets/2466bf75-f890-4c69-a8bb-88b323f51c3e">

Add the library to the list of your project dependencies. (No additional configuration is needed)

```
   <dependency>
      <groupId>org.springdoc</groupId>
      <artifactId>springdoc-openapi-starter-webmvc-api</artifactId>
      <version>2.6.0</version>
   </dependency>
```

In SpringBoot projects, all we need is the dependency & we'll automatically have SwaggerUI.

Start the application & go to "*localhost:8080/swagger-ui/index.html#/*". 

By default, it takes the URL of the default server that we have.

If we want to expose API documentation to multiple environments, we can specify the list of servers.

<img width="579" alt="Screenshot 2024-07-27 at 8 51 32 PM" src="https://github.com/user-attachments/assets/0c6f8b60-c1bb-42b1-a231-8ce4214de553">

-----------
#### Note that with security, with might come across an error,

<img width="877" alt="Screenshot 2024-07-27 at 8 42 48 PM" src="https://github.com/user-attachments/assets/34199ed4-ebd6-49ec-9906-d4d5a7133afb">
-----------

**Without security**, it will work just fine. We can see the UI representation.

#### This the the Rest API specification.

<img width="1143" alt="Screenshot 2024-07-27 at 8 47 36 PM" src="https://github.com/user-attachments/assets/283f5529-6b36-4304-8a13-7588b28d172d">

#### API definitions. It's the JSON representation of what we saw earlier.

<img width="937" alt="Screenshot 2024-07-27 at 8 48 38 PM" src="https://github.com/user-attachments/assets/35c24f48-7478-4c6b-8b4d-a3832bcf171b">

#### How does it work?

It scans our applications and reads all the resources & endpoints that we have. It scans for "Controller" or "RestControllers" that we have 
& displays them one by one.

<img width="1132" alt="Screenshot 2024-07-27 at 8 53 58 PM" src="https://github.com/user-attachments/assets/4d2453b1-4c39-488c-b6fb-514eff753a09">

To the bottom, we have a *Schema* block. It automatically scans all the "objects" that we use.

<img width="1093" alt="Screenshot 2024-07-27 at 8 55 09 PM" src="https://github.com/user-attachments/assets/26988aff-2ede-4cba-b3a6-abd584f23f43">
<img width="1116" alt="Screenshot 2024-07-27 at 8 55 20 PM" src="https://github.com/user-attachments/assets/3f4b165d-d8de-4c5e-8683-f373e2fef35c">



















