# Spring Cloud

Spring Cloud is an open-source platform designed to simplify the development and deployment of cloud-centric applications. It builds upon the popular Spring Framework and provides a set 
of tools and libraries to help developers create robust, scalable, and maintainable cloud-based systems. Spring Cloud offers a wide range of features, including configuration management,
service registration and discovery, circuit breakers, and distributed transactions. It also supports various cloud platforms, such as AWS, Azure, and Google Cloud Platform, making it a 
popular choice for organizations looking to build cloud-native applications.  

<img width="993" alt="Screenshot 2024-07-10 at 9 42 37 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d054fa4f-84fd-4d9c-a19a-7bdd7f63a290">
<img width="1175" alt="Screenshot 2024-07-10 at 9 44 25 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ba6fdf9a-fc79-4f80-8f81-a8dd9dff1682">

# Project Setup

We'll consider two microservices, emp-service & address-service, and then look into how they can communicate with each other.

### Dependencies required

```
  <dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-data-jpa</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-devtools</artifactId>
			<scope>runtime</scope>
			<optional>true</optional>
		</dependency>
		<dependency>
			<groupId>com.mysql</groupId>
			<artifactId>mysql-connector-j</artifactId>
			<scope>runtime</scope>
		</dependency>
		<!-- https://mvnrepository.com/artifact/org.modelmapper/modelmapper -->
		<dependency>
			<groupId>org.modelmapper</groupId>
			<artifactId>modelmapper</artifactId>
			<version>3.2.0</version>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
	</dependencies>

	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>
```

### 1. emp-service
<img width="1042" alt="Screenshot 2024-07-11 at 10 17 59 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/715665a3-3728-4d7a-94e8-88b92332a7d2">

- Consider a table named "employee" in db.

  <img width="739" alt="Screenshot 2024-07-11 at 10 28 01 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9c17a7a4-137d-4c9b-a0dc-b741eea1ad9b">

- Create a model-object/entity named *Employee* with the following properties

  <img width="1013" alt="Screenshot 2024-07-11 at 10 19 36 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/388ba12e-21d0-4472-bc22-2ec6f20b6727">

- Introducing ModelMapper

  We can send EmployeeResponse rather than Employee object directly.

  <img width="1103" alt="Screenshot 2024-07-11 at 8 00 08 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/92654c30-12cd-4888-8178-ec9cfc07c5ac">
  <img width="1033" alt="Screenshot 2024-07-11 at 10 23 31 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/094ddcdf-797f-4281-b0f4-cf02a683328f">

  #### EmployeeService

  <img width="870" alt="Screenshot 2024-07-11 at 8 02 10 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/48d9f3da-db62-4b0f-a3bc-818554116320">

  It's a hassle to set all the properties manually. We can use ModelMapper instead.

  <img width="716" alt="Screenshot 2024-07-11 at 8 10 09 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/f6673cde-d5c1-4dce-9cdf-00fbf4a6f8e4">
  <img width="1040" alt="Screenshot 2024-07-11 at 10 24 22 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c952dc91-4af5-452c-b375-93599e0b7094">

- Create EmployeeController that take an id and gets all Employee details.

  *Note: It's a good practice to send ResponseEntity*

  <img width="1050" alt="Screenshot 2024-07-11 at 10 24 28 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/36f7821b-76a7-4283-8662-e1567fe56ca3">

  We might come across an error. 

  *Note: Third party API's wont be auto-configured. We need to configure it manually.*

  <img width="878" alt="Screenshot 2024-07-11 at 8 16 14 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8cc4e360-3d90-4e89-984e-e218a7262e19">
  <img width="1046" alt="Screenshot 2024-07-11 at 10 25 29 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c364b155-3bfc-4a88-a548-8c096489ae9f">

- Add db details in application.properties

  <img width="1030" alt="Screenshot 2024-07-11 at 10 26 34 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/5564a8ed-d1c8-4d44-aaae-891b7b7e078d">

  Run the Application.

  ### IMPORTANT
  *Note: We might come across a Dialect error. In that case, add these two properties as well.*

  ```
  spring.jpa.properties.hibernate.temp.use_jdbc_metadata_defaults=false
  spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQLDialect
  ```

  <img width="1039" alt="Screenshot 2024-07-11 at 10 26 41 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/646cf797-dd36-4920-a58c-949b32ff1e04">
  <img width="1383" alt="Screenshot 2024-07-11 at 10 30 15 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9c5e8dcd-4fed-4aba-ae98-cc0c41f4c966">

### 2. address-service

- Similar to employee, create a table for address

  <img width="747" alt="Screenshot 2024-07-11 at 10 31 30 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/70cd9377-a286-41bb-a366-1836be45b8e4">

  We need address based on employee id.

  <img width="742" alt="Screenshot 2024-07-11 at 10 33 20 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/18a770ca-4a3d-4f6e-9da7-3a0ba482b20d">

- Entity *Address*

  <img width="1115" alt="Screenshot 2024-07-11 at 11 38 36 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/921ee75a-5484-4954-b323-8c87169d95ee">

- AddressResponse

  <img width="1085" alt="Screenshot 2024-07-11 at 11 38 50 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/6ceb9d03-723d-4861-9cbf-a2fe8298e9e1">

- AddressRepo

  <img width="1155" alt="Screenshot 2024-07-11 at 10 01 52 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7d2980c1-6265-4808-983e-3845aed7b3e2">
  <img width="1296" alt="Screenshot 2024-07-11 at 11 38 20 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a3f99ad1-775e-488a-a2b9-9ac614220016">

- AddressService

  <img width="1122" alt="Screenshot 2024-07-11 at 10 34 38 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2dd38c10-c61a-4a25-b7d8-0a2e83c67c79">

- AddressController

  <img width="1128" alt="Screenshot 2024-07-11 at 10 34 44 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/091a2ce7-9539-4a47-836b-8419a3869544">

- application.properties

  <img width="1130" alt="Screenshot 2024-07-11 at 10 36 07 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/fb001e98-c392-444a-8072-be032d646885">



  

