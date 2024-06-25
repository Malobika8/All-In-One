## SPRING DATA JPA

Let's come back to the Question,

##### Why cant we use autowired with EntityManager?  

We actually *can* use using SpringDataJPA. 

--------
Spring Data JPA focuses on using JPA to store data in a Relational Database. Its most compelling feature is the ability to create Repository
implementations automatically, at runtime, from a Repository Interface.

--------

Before that, let's add the dependency.

<!-- https://mvnrepository.com/artifact/org.springframework.data/spring-data-jpa -->
    <dependency>
      <groupId>org.springframework.data</groupId>
      <artifactId>spring-data-jpa</artifactId>
      <version>3.3.0</version>
    </dependency>

We need to use a special annotation over DBConfig i.e. @EnableJpaRepositories

<img width="1050" alt="Screenshot 2024-06-25 at 11 16 53 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9374d579-99d0-4223-92ae-ba8c434dd705">
<img width="839" alt="Screenshot 2024-06-25 at 11 20 44 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/36ea805d-b985-4bdc-a71f-508a8b8c1440">

Run the Application & it should work now.

<img width="742" alt="Screenshot 2024-06-25 at 11 21 44 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/11c24b22-4788-46d1-96fe-6d079cac0fa3">

Now the thing is, we might have different requirements(fetch a particular student OR fetch all students & many more) for which we would need to develop different methods. 

<img width="891" alt="Screenshot 2024-06-24 at 11 00 37 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/fc0ae8db-290e-4a93-b8fb-989fc7043d3e">
<img width="840" alt="Screenshot 2024-06-24 at 11 01 57 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8a19ca7c-48d4-46c2-b622-1fd3b82fe6fd">
<img width="860" alt="Screenshot 2024-06-24 at 11 03 30 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7d627d81-b09c-462e-b1a1-75972bf37fac">
<img width="806" alt="Screenshot 2024-06-24 at 11 03 37 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/df177e39-0c56-424b-aa27-d934bae7f46f">
<img width="885" alt="Screenshot 2024-06-24 at 11 03 57 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a56580ff-cbae-4bff-842f-a382811b09ca">

Instead, we can let our DAO(StudentDAO) extend JPARepository.

<img width="901" alt="Screenshot 2024-06-24 at 11 04 33 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/44a03960-0ae0-4bf8-9e5b-d82d0197314c">
<img width="852" alt="Screenshot 2024-06-25 at 11 27 22 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8863f1cf-03ec-4848-a0f1-3d414e667ca6">

Now, we won't really have to code inorder to do any CRUD operations.

<img width="1094" alt="Screenshot 2024-06-24 at 11 06 27 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/393fe05d-a475-4ed6-af4a-a1e8560043bc">

