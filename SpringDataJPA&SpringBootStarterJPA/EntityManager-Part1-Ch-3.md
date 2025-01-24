## Let's try to save some data into the Database

1. Create a Student object in main method.

   <img width="828" alt="Screenshot 2024-06-25 at 7 01 11 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ba2a8895-4445-4338-915b-d77e35add29f">

   In order to save, we would require a DataSource. Our Application needs to connect to the Database first.

   ##### Apart from this, what methods would we require to save data?

   *EntityManager.persist* method.

         In JPA, the EntityManager Interface is used to allow Applications to manage and search for Entities in the Relational Database. It           is a central object that represents a Connection to a Database. It is used to interact with the Database, allowing us to perform             CRUD (Create, Read, Update, Delete) operations on Entities. The EntityManager is responsible for managing Entity instances,                  persisting and retrieving them from the Database, and maintaining the Entity's lifecycle. It also provides various methods for               querying the Database, such as JPQL (Java Persistence Query Language) and criteria queries. The EntityManager is typically obtained          from a persistence unit and is used to manage Entities in a JPA-enabled Application.  

   ##### Where to check for Entitymanager?

   Java Persistence API

3. Create a DAO class which will implement **save** data.

   <img width="932" alt="Screenshot 2024-06-25 at 7 07 38 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/234dc6f5-d1ea-4172-9531-d4808668d637">

   We want Spring to create the EntityManager object. Hence, we would now require Spring dependency onto our Project.

   <!-- https://mvnrepository.com/artifact/org.springframework/spring-context -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>6.1.8</version>
        </dependency>

   Let's try it to save an object.

   <img width="1062" alt="Screenshot 2024-06-25 at 7 13 16 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/bda9c590-f3b2-4cc2-84f4-d259a0a9385b">

   ##### Errors

   <img width="1111" alt="Screenshot 2024-06-25 at 7 15 10 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/296612dd-23dc-4580-9129-37033b793f0e">
   <img width="1110" alt="Screenshot 2024-06-25 at 7 17 29 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b29a73d9-7d79-4292-84d4-77a3cdd20682">

   ##### What went wrong?

   <img width="1153" alt="Screenshot 2024-06-24 at 9 24 12 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/45bf7c94-1f9e-4516-ad0e-bd2bd657e336">

   We cannot create EntityManager directly. We would require EntityManagerFactory to create EntityManager. 

   <img width="766" alt="Screenshot 2024-06-25 at 7 22 54 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/57a1d112-ee87-4bb9-9be8-93f6cb146093">

   ---------------
   EntityManagerFactory provides instances of EntityManager for connecting to same database. It acts as a Container for Entity                 managers, allowing us to create, find, and manipulate Entities in our Application. When we start a new Transaction, the                     EntityManagerFactory is used to create a new EntityManager, which is used to manage the persistence context. The                            EntityManagerFactory is responsible for setting up the persistence unit, which includes configuring the Database Connection, mapping        Entities to tables, and defining the query language. It is typically used with a JPA provider like Hibernate or EclipseLink.

   --------------
  
   ##### How to create EntityManagerFactory? 
  
   Since we are using Spring, we can use a Class called *LocalContainerEntityManagerFactoryBean* to create EntityManagerFactory.
   In Spring, *LocalContainerEntityManagerFactoryBean* helps us create EntityManagaerFactory.

   <img width="837" alt="Screenshot 2024-06-24 at 9 57 51 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c813d268-c8c4-496d-b653-030a11a42019">
   <img width="1134" alt="Screenshot 2024-06-24 at 10 00 30 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7dfc0f8e-26dc-4ade-998d-7c8c1696f2f5">

   ##### What should be the next step then?

   <img width="963" alt="Screenshot 2024-06-24 at 10 00 53 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/591aab0d-48dd-4edd-9442-f091290dcfb0">

   We need to add Spring support to JPA.
  
   Let's add the Dependency

   <!-- https://mvnrepository.com/artifact/org.springframework/spring-orm -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-orm</artifactId>
            <version>6.1.8</version>
        </dependency>

3. Create bean for EntityManagerFactory.

   There are 2 Local-EntityManagerFactoryBean
   - LocalContainerEntityManagerFactoryBean: This can be used with Container based Applications. (Spring provides us Container) 
   - LocalEntityManagerFactoryBean: This can be used with Standalone Applications.

     <img width="269" alt="Screenshot 2024-06-25 at 8 00 37 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/4995e1e6-2a45-4ab9-9447-2c1d04d253b8">

   We need to add packages which needs to be scanned for Entities.

   -----------------
   **Note:** ComponentScan won't scan Entities. We need to tell EntityManager where our Entities are present. For this, we can use             entityManagerFactoryBean.setPackagesToScan("com.springjpa.entity");
   
   OR
   
   There's an annotation that can be used to achieve the same.
   
   -----------------

   <img width="1030" alt="Screenshot 2024-06-25 at 8 09 20 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/43d70d23-168b-4c22-a9d0-2d02f98ccb32">

   Let's try to Run the Application.

   #### Error

   <img width="1104" alt="Screenshot 2024-06-25 at 8 10 49 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8c5f80a0-ba80-4c3b-8d33-5b923f5345b2">

   We need to mention the Provider.

   <img width="962" alt="Screenshot 2024-06-25 at 8 20 27 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/6c48272e-f6a0-47a2-9bdc-7fc6bb9b6856">

   Let's try to run again.

   #### Error

   <img width="1109" alt="Screenshot 2024-06-24 at 10 24 37 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c2ca83f5-fe96-4c81-9582-840e01e57cfb">
    
   Add hibernate dependency

   <!-- https://mvnrepository.com/artifact/org.hibernate.orm/hibernate-core -->
        <dependency>
            <groupId>org.hibernate.orm</groupId>
            <artifactId>hibernate-core</artifactId>
            <version>6.5.2.Final</version>
        </dependency>
   
   Let's try to run again.

   #### Error

   <img width="1082" alt="Screenshot 2024-06-25 at 8 29 20 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ea7f2324-797c-4c15-a052-43c00413bccc">

   We need to add Dependency for mysql driver.

   <!-- https://mvnrepository.com/artifact/com.mysql/mysql-connector-j -->
        <dependency>
            <groupId>com.mysql</groupId>
            <artifactId>mysql-connector-j</artifactId>
            <version>8.4.0</version>
        </dependency>

   Let's try to run again.

   #### Error

   The EntityManager is not getting AutoWired.
   
   <img width="1108" alt="Screenshot 2024-06-25 at 8 32 39 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/1240d5ca-dce2-49bd-b69d-2522eb027bfc">
   <img width="1105" alt="Screenshot 2024-06-24 at 10 27 03 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c6e6ce67-c1f5-44bb-98a9-e9cb32aba2ff">

   ##### Should we create a EntityManager bean on our own then?

   <img width="912" alt="Screenshot 2024-06-25 at 8 44 45 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9a37b4b3-1b70-40b3-9394-e32a68329430">

   Let's try to run the Application and see if EntityManager bean is injected now.

   <img width="926" alt="Screenshot 2024-06-25 at 8 46 03 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7283ff22-f8d9-4e68-ad16-45a62e63930a">

   It says "record inserted".

   Let's check the Database to confirm.

   <img width="702" alt="Screenshot 2024-06-24 at 10 29 10 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d5261d88-fcee-4fc7-833b-08f030dc1dea">

   Looks like it didn't really insert the data succesfully.

    



    


    



  
