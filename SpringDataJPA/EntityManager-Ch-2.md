## Let's try to save some data into the Database

1. Create a Student object in main method.

   <img width="828" alt="Screenshot 2024-06-25 at 7 01 11 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ba2a8895-4445-4338-915b-d77e35add29f">

   In order to save, we would require a DataSource. Our Application needs to connect to the Database first.

   ##### Apart from this, what methods would we require to save data?

   *EntityManager.persist* method.

   ##### Where to check for Entitymanager?

   Java Persistence API

2. Create a DAO class which will implement **save** data.

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

  ##### What happened?

  <img width="1153" alt="Screenshot 2024-06-24 at 9 24 12 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/45bf7c94-1f9e-4516-ad0e-bd2bd657e336">

  We cannot create EntityManager directly. We would require EntityManagerFactory to create EntityManager. 

  <img width="766" alt="Screenshot 2024-06-25 at 7 22 54 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/57a1d112-ee87-4bb9-9be8-93f6cb146093">
  
  ##### How to create EntityManagerFactory? 
  
  Since we are using Spring, we can use a Class called *LocalContainerEntityManagerFactoryBean* to create EntityManagerFactory.

  <img width="837" alt="Screenshot 2024-06-24 at 9 57 51 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c813d268-c8c4-496d-b653-030a11a42019">
  <img width="1134" alt="Screenshot 2024-06-24 at 10 00 30 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7dfc0f8e-26dc-4ade-998d-7c8c1696f2f5">

  ##### What should be the next step then?

  <img width="963" alt="Screenshot 2024-06-24 at 10 00 53 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/591aab0d-48dd-4edd-9442-f091290dcfb0">

  Let's add the dependency

  <!-- https://mvnrepository.com/artifact/org.springframework/spring-orm -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-orm</artifactId>
            <version>6.1.8</version>
        </dependency>

  

  
