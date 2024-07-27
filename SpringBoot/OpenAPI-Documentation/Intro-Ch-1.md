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

# Configure & add properties & make customization on the OpenAPI definition

We will use annotations to configure everything or to give more of definitions & properties to our API

We can add the annotations on the main Application.

<img width="744" alt="Screenshot 2024-07-27 at 8 58 18 PM" src="https://github.com/user-attachments/assets/c3f2a21f-6de3-4078-a58e-6a88aa3e6da5">

We can separate things as well. We can create a new class called APIConfig. It will be an empty class with just annotations.

"*@OpenAPIDefinition*"

<img width="1081" alt="Screenshot 2024-07-27 at 9 00 06 PM" src="https://github.com/user-attachments/assets/bf95482e-e29b-41bc-99d6-ec5fb88f34ee">

Info annotation has a list of properties.

<img width="955" alt="Screenshot 2024-07-27 at 8 59 46 PM" src="https://github.com/user-attachments/assets/05c83ed3-8c05-4302-aea8-bd4a077b31cd">
<img width="1077" alt="Screenshot 2024-07-27 at 9 04 26 PM" src="https://github.com/user-attachments/assets/38d9430e-aae9-4608-a745-b165add5dddd">
<img width="1081" alt="Screenshot 2024-07-27 at 9 05 44 PM" src="https://github.com/user-attachments/assets/8c8df81d-5ca1-48af-817e-399302a18bb0">

Restart the Application

<img width="1145" alt="Screenshot 2024-07-27 at 9 06 21 PM" src="https://github.com/user-attachments/assets/79939b79-40d8-4094-92f4-23d4945a721d">
<img width="776" alt="Screenshot 2024-07-27 at 9 06 42 PM" src="https://github.com/user-attachments/assets/158611dd-df43-4505-8527-e4a44f8e2867">

# Let's try a Request

Configure OpenAPI to accept Bearer Token

<img width="1038" alt="Screenshot 2024-07-27 at 9 10 29 PM" src="https://github.com/user-attachments/assets/71aacc8c-d964-449f-989f-fade1f498e51">

Specify security requirements for our API

- We can add it at the Controller level (we can have different requirements for different Controllers)

  <img width="1029" alt="Screenshot 2024-07-27 at 9 14 06 PM" src="https://github.com/user-attachments/assets/1d7b5aeb-5b20-4104-a044-fed829411bf6">

- We can add it to the separate config class that we created. (Global level for all Controllers)

  <img width="1023" alt="Screenshot 2024-07-27 at 9 17 24 PM" src="https://github.com/user-attachments/assets/9a9cabe7-fd52-4a9f-894f-4fb10c46fe1f">

Restart the Application

<img width="1128" alt="Screenshot 2024-07-27 at 9 11 05 PM" src="https://github.com/user-attachments/assets/cd187c1c-e812-46a2-bfe3-cadebb930ba3">
<img width="769" alt="Screenshot 2024-07-27 at 9 11 12 PM" src="https://github.com/user-attachments/assets/20a600a3-7716-4ee4-bc76-74bc41b1c705">
<img width="1136" alt="Screenshot 2024-07-27 at 9 19 21 PM" src="https://github.com/user-attachments/assets/c7d9185a-5a76-4da3-8689-a00eb1f488d4">
<img width="1129" alt="Screenshot 2024-07-27 at 9 19 28 PM" src="https://github.com/user-attachments/assets/0590c7ba-d107-40ee-9ca7-8a15960bdb64">
<img width="1098" alt="Screenshot 2024-07-27 at 9 19 41 PM" src="https://github.com/user-attachments/assets/de61d7db-3908-4a00-a49c-0c849fa50e73">

We can see the lock icons (when done at the Controller level)

<img width="1133" alt="Screenshot 2024-07-27 at 9 15 13 PM" src="https://github.com/user-attachments/assets/aa960c4e-f6a9-4532-9b95-95b9b4d0a36a">

<img width="1099" alt="Screenshot 2024-07-27 at 9 16 20 PM" src="https://github.com/user-attachments/assets/bdf30f06-2e94-4646-96b0-390466cc9795">

# Enhancement

* Change the Controller name displayed in SwaggerUI:

  <img width="1031" alt="Screenshot 2024-07-27 at 9 21 30 PM" src="https://github.com/user-attachments/assets/7535ec69-6e4a-460a-af17-c4511933b55e">
  <img width="1138" alt="Screenshot 2024-07-27 at 9 33 08 PM" src="https://github.com/user-attachments/assets/38185a37-6a83-43ee-bea0-f7ae68709e28">

* Add description/summary to endpoints:

  <img width="1061" alt="Screenshot 2024-07-27 at 9 23 46 PM" src="https://github.com/user-attachments/assets/c2faced9-88fc-4ba8-9517-081cd65f3ac1">
  <img width="1055" alt="Screenshot 2024-07-27 at 9 24 03 PM" src="https://github.com/user-attachments/assets/b5f41536-215b-4762-bb7a-36ad6d8c514a">

  Restart the Application

  <img width="1130" alt="Screenshot 2024-07-27 at 9 26 34 PM" src="https://github.com/user-attachments/assets/2a005f33-2bcd-47b5-ba84-b412c5943e15">
  <img width="1114" alt="Screenshot 2024-07-27 at 9 26 48 PM" src="https://github.com/user-attachments/assets/6b5e0695-a9d9-4bf7-a4bd-39fc5ed36dd1">

* Suppose a Controller is there only for internal usage and doesn't want to expose the endpoints for others. 

  <img width="747" alt="Screenshot 2024-07-27 at 9 32 45 PM" src="https://github.com/user-attachments/assets/aae197a7-0234-4142-9638-bf8eb6bb9ae6">

  We no longer have "DemoController"

  <img width="1138" alt="Screenshot 2024-07-27 at 9 33 08 PM" src="https://github.com/user-attachments/assets/b443322e-3c86-427d-b77d-8b23a0bfeb7d">

* Hide some operations like "POST", "DELETE" & "PUT" mappings. So, the outside world can only use "GET" operation.

  <img width="905" alt="Screenshot 2024-07-27 at 9 30 30 PM" src="https://github.com/user-attachments/assets/4aa01da3-f97e-42ff-a119-c8a33f3ea9b1">
  <img width="1130" alt="Screenshot 2024-07-27 at 9 31 39 PM" src="https://github.com/user-attachments/assets/e0019d93-982f-4fc2-a7d6-5e905b8a6d2c">













