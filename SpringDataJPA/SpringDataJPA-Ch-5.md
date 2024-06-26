# Spring Data JPA

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
<img width="540" alt="Screenshot 2024-06-26 at 8 14 01 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7539d0a1-eef3-4f2e-b4bb-20c09c9650fa">

Instead, we can let our DAO(StudentDAO) extend JPARepository.

<img width="901" alt="Screenshot 2024-06-24 at 11 04 33 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/44a03960-0ae0-4bf8-9e5b-d82d0197314c">
<img width="852" alt="Screenshot 2024-06-25 at 11 27 22 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8863f1cf-03ec-4848-a0f1-3d414e667ca6">
<img width="1147" alt="Screenshot 2024-06-26 at 8 14 32 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c2d4f723-81da-4436-b8aa-896fb5330cd5">
<img width="1129" alt="Screenshot 2024-06-26 at 8 14 58 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/fbecb1d4-c3de-4a5c-b517-cc9a1e27e36b">

Now, we won't really have to code inorder to do any CRUD operations.

<img width="1094" alt="Screenshot 2024-06-24 at 11 06 27 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/393fe05d-a475-4ed6-af4a-a1e8560043bc">
<img width="1123" alt="Screenshot 2024-06-26 at 8 18 03 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/dac22b47-9dfd-4726-be36-a5a4b9343c13">

JpaRepository internally extends Respository.

<img width="1099" alt="Screenshot 2024-06-26 at 8 17 19 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/f62c306e-dded-4340-9509-ae487b0d2c15">

Our Interface gets access to multiple methods already present in JpaRepository(some comes from parent which it extends).

<img width="1145" alt="Screenshot 2024-06-26 at 8 22 03 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2b82de47-789f-4335-9cac-f3e2cb43870f">
<img width="747" alt="Screenshot 2024-06-26 at 8 28 19 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/28205b19-57e2-4260-9e1c-493bfbf8ffa2">

##### But JpaRepository is an interface right? Who provides the implementation?

Spring provides implementation for us.

<img width="1092" alt="Screenshot 2024-06-26 at 8 33 47 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a5b187f2-533d-48d1-8634-9ab09a7abf68">
<img width="1147" alt="Screenshot 2024-06-26 at 8 34 26 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/43d98cd8-ac5f-4bc3-b4a4-e7060edd2023">

We need to use *@EnableJpaRepository* annotation to generate Repository implementation by Spring.

<img width="1150" alt="Screenshot 2024-06-26 at 8 23 33 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/e4f0b176-1587-4993-b021-b27f32be54dc">

OR

<img width="963" alt="Screenshot 2024-06-26 at 8 26 35 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2eaf6509-479b-473c-881d-74fc1d156167">

We can then simply call the method as per our requirement.

<img width="958" alt="Screenshot 2024-06-26 at 8 29 45 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/fa7e05f7-23a0-435f-8aa2-d3cfc1f998c7">

#### Note

Similar to Entity, Repository class won't be scanned as well by ComponentScan. We need to mention packages to scan in both of the cases.

#### Crux of the Story

<img width="1157" alt="Screenshot 2024-06-26 at 8 48 25 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7721ec43-b887-4dce-8a3c-ce1c7d656575">


