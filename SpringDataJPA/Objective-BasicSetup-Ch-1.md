## Objective

To create a simple Application which can save data to a Database using Spring, JPA, Spring Data JPA initially & later switching to SpringBoot.

##### Let's begin

1) Create a Maven project. Use maven-archetype-quickstart.

   <img width="801" alt="Screenshot 2024-06-24 at 8 57 43 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b70a3ab1-52fe-4b55-8638-d43592c024d0">

2) Add Dependency: We initially need to add JPA dependency.

   #### What is JPA?
   The Java Persistence API (JPA) is a specification of Java. It is used to persist data between Java object and relational      database.      JPA acts as a bridge between object-oriented domain models and relational database systems.
   As JPA is just a specification, it doesn't perform any operation by itself. It requires an implementation. So, ORM tools like Hibernate,     TopLink and iBatis implements JPA specifications for data persistence.
   
   <!-- https://mvnrepository.com/artifact/jakarta.persistence/jakarta.persistence-api -->
        <dependency>
            <groupId>jakarta.persistence</groupId>
            <artifactId>jakarta.persistence-api</artifactId>
            <version>3.2.0</version>
        </dependency>

   Other required dependencies. (Note: We'll be adding it as and when required)
   
   <!-- https://mvnrepository.com/artifact/org.springframework/spring-context -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>6.1.8</version>
        </dependency>
   <!-- https://mvnrepository.com/artifact/org.springframework/spring-orm -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-orm</artifactId>
            <version>6.1.8</version>
        </dependency>
   <!-- https://mvnrepository.com/artifact/org.hibernate.orm/hibernate-core -->
        <dependency>
            <groupId>org.hibernate.orm</groupId>
            <artifactId>hibernate-core</artifactId>
            <version>6.5.2.Final</version>
        </dependency>
   <!-- https://mvnrepository.com/artifact/com.mysql/mysql-connector-j -->
        <dependency>
            <groupId>com.mysql</groupId>
            <artifactId>mysql-connector-j</artifactId>
            <version>8.4.0</version>
        </dependency>
   <!-- https://mvnrepository.com/artifact/org.springframework.data/spring-data-jpa -->
        <dependency>
            <groupId>org.springframework.data</groupId>
            <artifactId>spring-data-jpa</artifactId>
            <version>3.3.0</version>
        </dependency>

4) Create a simple Student Entity class. Add getters, setters and toString method.

   <img width="1025" alt="Screenshot 2024-06-24 at 9 10 23 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/40bb841b-6767-4181-9d77-21d512c4f74d">

5) Create a Configuration class using which the Container would be created.

   <img width="1023" alt="Screenshot 2024-06-25 at 6 32 00 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a9d0ff2a-5b26-4d67-8a09-f286f677bf7e">


## IMPORTANT

We might come across an error 

-----
      Spring Boot 3.2.2: EntityManagerFactory interface org.hibernate.SessionFactory seems to conflict with Spring's EntityManagerFactoryInfo mixin

-----

### Fix:

It is probably due to using Jakarta Persistence-API version 3.2.0-M1.

After changing Jakarta Persistence-API version from 3.2.0-M1 to 3.1.0 in Maven pom.xml (according to Spring Boot migration guide, v3.1.0 is the default version supported by Spring Boot 3.2.x), the previously thrown exception concerning Spring Data JPA/Hibernate/Jakarta incompatibility no longer occurs.
