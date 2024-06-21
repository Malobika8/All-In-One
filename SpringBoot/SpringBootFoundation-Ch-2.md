## Spring Boot Features

### Pre-requisites - Should know the following

<img width="1037" alt="Screenshot 2024-06-21 at 6 58 31 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/4ae4065b-49c8-422a-b64a-533dd31b4991">
<img width="1037" alt="Screenshot 2024-06-21 at 6 58 50 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/118253e4-4e70-49f9-8c15-fcae84215b3a">
<img width="1037" alt="Screenshot 2024-06-21 at 6 59 13 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/3dd0b244-01d8-4d0f-9646-cfb35a846424">

# Let's try to build a basic SpringBoot App from scratch

1) Create a new maven project
2) Modify project to make it a Spring Web Application: There are multiple dependencies that needs to be added like spring-
   webmvc that helps in building spring web project.

   <img width="787" alt="Screenshot 2024-06-21 at 8 07 11 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ef085146-1135-4f6e-a17c-2ae8254f2e84">
   <img width="1119" alt="Screenshot 2024-06-21 at 8 07 18 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/32f29e9d-9c63-4bb6-b307-6fa4c5407545">

   But apart from spring-webmvc, there are multiple other dependencies that are required. Instead of adding all of these one at a time, we can
   make use of a SpringBoot feature.

   Add the below dependency

   <!-- https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-web -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
            <version>3.3.0</version>
        </dependency>

    Spring adds a lot of other jars which might be required to develop a web application. All of them are bundled with spring-boot-starter-web.

    <img width="270" alt="Screenshot 2024-06-21 at 8 30 18 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/1a0d3670-1a53-4db7-8951-4109541f1773">
    <img width="830" alt="Screenshot 2024-06-21 at 8 32 04 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/93373a23-fc48-463d-be33-6e650749466e">
    <img width="783" alt="Screenshot 2024-06-21 at 8 32 53 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/5e8bf60c-a0cc-4b25-a801-1eaab1c5c1e4">
    <img width="804" alt="Screenshot 2024-06-21 at 8 33 21 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/65306ed4-60df-4da9-964a-4ed6d6562c04">

    Apart from these, there are different versions that we have to manage and their compatibility. 

    <img width="675" alt="Screenshot 2024-06-21 at 8 33 56 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/3c40ae3e-6ac5-40c1-b11d-11a2775f43f7">
    <img width="1084" alt="Screenshot 2024-06-21 at 8 34 07 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ed933b00-5bcc-4cfd-b8ca-14abee9251b2">
    <img width="918" alt="Screenshot 2024-06-21 at 8 36 00 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/84b05946-0f08-4db4-8499-0bcc0c4a2890">

    Spring boot has another feature that takes care of version management as well.

    Add the below dependency out of the *dependencies* section with *parent* tag.

    <!-- https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-parent -->
       <dependency>
          <groupId>org.springframework.boot</groupId>
          <artifactId>spring-boot-starter-parent</artifactId>
          <version>3.3.0</version>
          <type>pom</type>
        </dependency>

   Whatever version we specify will be the SpringBoot version and all other dependencies will have the versions inherited from the version mentioned
   in parent project (spring-boot-starter-project).

   <img width="1105" alt="Screenshot 2024-06-21 at 8 41 58 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/de545497-194c-4325-9064-c94a843c2ff3">

   Note that parent is not a dependency but acts as version manager.

   <img width="1031" alt="Screenshot 2024-06-21 at 8 44 17 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b12d904b-196a-4a4b-855d-76ea98d579c1">
   <img width="838" alt="Screenshot 2024-06-21 at 8 45 46 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a4977b11-a0e9-4e1d-a37d-84f6e2f9df07">

   In dependencies section, we can add different other projects which can be used with current project.

   With this, our SpringBoot project setup is done.

3) Create a simple Controller

   <img width="1100" alt="Screenshot 2024-06-21 at 8 48 06 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/f5e2aca3-c16c-4666-a984-f921d21b8213">
   <img width="1019" alt="Screenshot 2024-06-21 at 8 52 35 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/053134fb-6f97-44d7-9806-e6b01997bae0">

   But how do we run the Application? - We have to create a main method or class which will run our Application. SpringApplication has a *run*
   method that helps in starting the project.

   <img width="910" alt="Screenshot 2024-06-21 at 8 59 42 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b6b02cde-dbf2-4369-96b3-e8967b47638e">

   When we run the main method, we come across an error.
   
   <img width="1350" alt="Screenshot 2024-06-21 at 9 00 33 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7a411db8-2f9a-405a-a993-e2f487231bc0">

   This is because we are required to mention source where all configurations are done. We can mention the "StarterApp" class as the source.
   This class can act as an entry point to our Application.

   When we run it, it throws another error.

   <img width="1339" alt="Screenshot 2024-06-21 at 9 04 55 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/0570bcf1-eb2e-4372-a78e-67927128c2d5">

   The run method attempts to create a container/context behind the scene. But while creating that container, something is failing.

   <img width="1206" alt="Screenshot 2024-06-21 at 9 06 20 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9836d036-e4a7-436c-bfd6-86039fd02c66">

   It is unable to start a web-server as it is trying to create a web-server.

   <img width="965" alt="Screenshot 2024-06-21 at 9 08 50 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/528688f7-1b31-4996-97c6-5b7f319eeb64">

   Spring is attempting to initialize the class(ServletWebServerFactory class helps in setting up a web server) but failing.

   <img width="770" alt="Screenshot 2024-06-21 at 9 11 43 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/eceab9dc-ef4a-4570-9eac-bc4542ac5e8f">

   We want Spring to configure things automatically. For this, we can use **@AutoConfiguration** annotation.

   The @EnableAutoConfiguration annotation enables Spring Boot to auto-configure the application context. Therefore, it automatically
   creates and registers beans based on both the included jar files in the classpath and the beans defined by us.
   When this annotation is used, Spring Boot will search for and apply the appropriate configuration, reducing the need for manual
   configuration of the application. The annotation is commonly used in Spring Boot applications to make the application context
   initialization process easier and more efficient.

   For example, when we define the spring-boot-starter-web dependency in our classpath, Spring boot auto-configures Tomcat and Spring MVC.
   However, this auto-configuration has less precedence in case we define our own configurations.

   <img width="843" alt="Screenshot 2024-06-21 at 9 13 03 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/87f76271-7fa1-4603-9b44-8f1be589a0a2">

   Let's try to run the application now.

   <img width="1344" alt="Screenshot 2024-06-21 at 9 17 40 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/55dd36c5-20a6-4a81-afcf-d515694254d4">

   However, the endpoint isn't working

   <img width="970" alt="Screenshot 2024-06-21 at 9 19 45 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/6e916637-cca6-4b91-82e8-16fcbda98c48">

   We need to do ComponentScan. It scans all the classes present in the package and checks if any of them has @Component, @Controller or @RestController
   etc. Spring creates object and keeps it in the container.

   @ComponentScan is an annotation used in the Spring Framework for auto-detecting and registering Spring-managed components (e.g. beans,
   controllers, services, repositories, etc.) within a specified package or set of packages. A component scan is a way to find classes
   to be injected in a Spring Boot application using annotations. In Spring Boot, component scans allow for the automatic discovery of
   components that can be injected into other classes in the application.
   Component scans are configured using the annotation *@EnableAutoConfiguration* and the annotation *@ComponentScan* on the main class of the
   application. This annotation specifies the base package to search for components to be injected.
   Component scans can be enabled in a Spring Boot application to reduce the amount of manual configuration required. They are useful for
   applications with many classes, as they can be used to automatically discover components that can be injected into other classes in the
   application.

   <img width="1024" alt="Screenshot 2024-06-21 at 9 31 43 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/5198c164-d353-4cae-b0a6-fcbdb0317aa2">

   Run the Application

   <img width="720" alt="Screenshot 2024-06-21 at 9 32 03 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/af645aa7-2565-4230-888e-1aeb80b89af9">

   
   
   
