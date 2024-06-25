## How to save data to the Database?

Since our objective is to do a database transaction, we would require a DataSource.

<img width="723" alt="Screenshot 2024-06-24 at 10 01 16 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/cc9d2b87-bf7b-4188-90b6-4ca5f37696ac">

1. Create a class called DBConfig.
   
   ##### How to create a Datasource in Spring?

   We would require *DriverManagerDataSource*.

   ##### What is it exactly?
   
   Simple implementation of the standard JDBC DataSource Interface, configuring the plain old JDBC DriverManager via bean properties, and
   returning a new Connection from every getConnection call. The DriverManagerDataSource is a class in Java that used to create a DataSource
   for a Database. It is a part of the Java Database Connectivity (JDBC) API and is used to manage Connections to a Database. The DriverManagerDataSource
   class is used to create a data source that can be used to connect to a database, and it provides methods for getting a connection to the
   Database, closing the Connection, and getting the Database metadata. It is commonly used in Java Applications that need to connect to a
   Database.

   We need to add Spring support to JPA.

   Dependency required:

   <!-- https://mvnrepository.com/artifact/org.springframework/spring-orm -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-orm</artifactId>
            <version>6.1.8</version>
        </dependency>
   
   The *spring-orm* dependency internally has *spring-jdbc* added.

   <img width="888" alt="Screenshot 2024-06-25 at 7 42 03 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/34e7fcac-9614-4c88-89c9-d22fecf1757f">
   <img width="1014" alt="Screenshot 2024-06-24 at 10 05 14 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/cd4c7e60-7f5e-43ba-b07a-6172353e2c61">

3. Let's try to create a Connection to the Database

   Create a bean for *DriverManagerDataSource*. We would require **url, username, password**.

   <img width="928" alt="Screenshot 2024-06-25 at 7 46 51 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/56187f1a-7bf3-4dec-b264-133647a9bfbb">

   #### Note:

       We should completely avoid using DriverManagerDataSource in Production as in real time, we require ConnectionPool.
       In our Application, a new Connection is created for every DB operation which is acceptable considering this is a simple Application.
       In Real Time, Connection is created using ConnectionPool. DriverManagerDataSource doesn't return any ConnectionPool.
       As already mentioned, our Application is quite simple which is the reason behind using DriverManagerDataSource.

   <img width="854" alt="Screenshot 2024-06-25 at 7 54 43 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/5a9cec4e-f345-4de8-ba4b-95a15186dce3">
   
    
