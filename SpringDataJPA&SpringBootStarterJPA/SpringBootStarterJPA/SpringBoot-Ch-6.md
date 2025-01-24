## Let's configure our project from Spring to SpringBoot

1. Dependencies:

   - spring-boot-starter-data-jpa: This provides all the dependencies that we added earlier.

     <!-- https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-data-jpa -->
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-data-jpa</artifactId>
              <version>3.3.0</version>
          </dependency>

  - mysql-connector 
     <!-- https://mvnrepository.com/artifact/com.mysql/mysql-connector-j -->
         <dependency>
              <groupId>com.mysql</groupId>
              <artifactId>mysql-connector-j</artifactId>
              <version>8.4.0</version>
         </dependency>

  - For versions, we can add spring-boot-starter-parent

      <!-- https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-parent -->
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-parent</artifactId>
              <version>3.3.0</version>
              <type>pom</type>
          </dependency>

    <img width="949" alt="Screenshot 2024-06-26 at 9 00 20 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9e48203a-9ea0-4e5f-a8d8-871851fb08ba">

2. Create a resource folder where we can have our DB Connection details.

   <img width="972" alt="Screenshot 2024-06-26 at 9 29 47 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/54e2bda4-a6f7-4ac4-bdce-a6c5609c330e">

3. Create container with *SpringApplication.run*
4. Spring should automatically enable configurations for us. We need to tell Spring to configure ComponentScan, DataSource, EntityManagerFactory
   TransactionManager etc.

   This can be done using *@SpringBootApplication* annotation.

   ------------------
   ### Student
   ------------------

   <img width="1024" alt="Screenshot 2024-06-26 at 9 24 40 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/97f10fa4-180f-47f8-a623-d54e1a852c39">

   ------------------
   #### StudentDAO
   ------------------

   <img width="994" alt="Screenshot 2024-06-26 at 9 24 47 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/5b2ddf1f-c60b-4cbb-82d8-6f553e269e69">

   ------------------
   #### Demo
   ------------------

   <img width="988" alt="Screenshot 2024-06-26 at 9 24 26 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a9dbf7eb-7fdd-48e8-b830-55733a029c80">

### Let's run the Application

<img width="1147" alt="Screenshot 2024-06-26 at 9 30 50 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7c1f12ad-531b-4bc4-b444-9809acaa3be5">

## FYI
We can activate debug using property in Application.properties: debug=true

<img width="798" alt="Screenshot 2024-06-26 at 9 38 40 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/56739268-f0f1-44db-8029-3f343e81295f">

We can see all configurations happening automatically behind the scene which we configured earlier when we just used Spring with JPA.

<img width="885" alt="Screenshot 2024-06-26 at 9 33 42 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c4c587cc-ee0d-45f5-8973-57678180d279">
<img width="906" alt="Screenshot 2024-06-26 at 9 34 35 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/4092c563-0cc6-4475-9742-861fb8677ef6">
<img width="910" alt="Screenshot 2024-06-26 at 9 35 17 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/1d728ea5-9c4c-438f-b3f5-3f8dfe5a3bc1">
<img width="911" alt="Screenshot 2024-06-26 at 9 35 26 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/503b85ec-281a-4be5-a4b2-d22d3baaefbf">

We can exclude some auto configurations as well if we want to configure by ourselves

<img width="785" alt="Screenshot 2024-06-26 at 9 36 26 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/df21ca60-e4d1-41a9-9505-858644163013">
<img width="877" alt="Screenshot 2024-06-26 at 9 36 35 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b8d22026-1e99-4811-8f93-d8708574706f">

## Good to Know
------------------
### @EntityScan
------------------

In SpringBoot, Entity and DAO automatically gets scanned. ComponentScan doesn't scann all these. If we follow the package convention(i.e. 
it should be in a sub-package of base-package), SpringBoot scans perfectly fine.

##### What if we don't follow the package convention?

Let's suppose we create a package named entity

<img width="338" alt="Screenshot 2024-06-26 at 9 45 02 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c2c4cf90-5a6e-4aa9-92c9-891e12fa98bf">

Now, if we run the Applicaton, it won't be able to find the Student entity

<img width="817" alt="Screenshot 2024-06-26 at 9 46 05 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/07e29843-0c33-4622-a6ba-fa82ce59bab1">
<img width="814" alt="Screenshot 2024-06-26 at 9 46 25 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/718d9b7c-8845-4ade-8042-95859adaf7e3">

To scan entities, we need to enable entity scanning

<img width="809" alt="Screenshot 2024-06-26 at 9 46 45 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/cfdb774a-97f0-4fde-9bad-e759705fb7b8">
<img width="820" alt="Screenshot 2024-06-26 at 9 49 01 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2c73b439-d040-4732-b979-0df12ea5c374">

------------------
### @EnableJpaRepositories
------------------

Similar is the case with JpaRepository

<img width="297" alt="Screenshot 2024-06-26 at 9 49 57 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/bd65cf1b-3889-4061-8836-8ec15f08c3a0">
<img width="821" alt="Screenshot 2024-06-26 at 9 50 32 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/bfe0b1db-a2a6-477b-a387-d745117a76de">
<img width="732" alt="Screenshot 2024-06-26 at 9 53 21 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/943559b6-e55d-45a9-a6f8-031e2ad6d01f">
<img width="822" alt="Screenshot 2024-06-26 at 9 54 09 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/3f6bfab3-861c-499e-8d4b-1d5e50d0aac0">

------------------
### What's inside Starter Data JPA?
------------------

<img width="1111" alt="Screenshot 2024-06-26 at 9 55 09 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c751c92c-57dd-47a1-b42b-7f1b4ce0416a">

This is a one stop solution as it pulls in all the required Dependencies

<img width="1112" alt="Screenshot 2024-06-26 at 9 55 43 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/600602b3-7278-4d2c-b630-db94d9652ec5">
<img width="1132" alt="Screenshot 2024-06-26 at 9 56 43 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c76725fb-4d3b-435f-b3f9-aaf69e02c055">

------------------
### How to show sql with Spring/SpringBoot projects?
------------------

- **Spring with JPA:** In normal Spring Application, we can set show sql to true while creating EntityManagerFactory.

  <img width="858" alt="Screenshot 2024-06-26 at 9 59 16 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/51c72b04-e7f0-41f5-8018-8b7626c2d215">

  We can see all the insert and select queries.

  <img width="892" alt="Screenshot 2024-06-26 at 10 00 18 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/5868f052-1246-4cfe-84a9-2e458f93e271">

- **SpringBoot:** Similarly, in SpringBoot, we can enable show sql by adding a property in Application.properties

  <img width="857" alt="Screenshot 2024-06-26 at 10 01 29 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/04cc88cc-1281-4f9c-a086-e5e941226bc7">
  <img width="912" alt="Screenshot 2024-06-26 at 10 02 00 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d0c2ab50-7710-46d4-b9ff-5daf7dd89ed8">




