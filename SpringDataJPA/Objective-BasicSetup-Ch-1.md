## Objective

To create an simple Application which can save data to a Database. Use Spring, JPA, Spring Data JPA initially. Switch later to SpringBoot.

##### Let's begin

1) Create a maven project. Use maven-archetype-quickstart.

   <img width="801" alt="Screenshot 2024-06-24 at 8 57 43 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b70a3ab1-52fe-4b55-8638-d43592c024d0">

2) Required dependencies. (Note: We'll observe which scenario requires which Dependency)

   <!-- https://mvnrepository.com/artifact/jakarta.persistence/jakarta.persistence-api -->
        <dependency>
            <groupId>jakarta.persistence</groupId>
            <artifactId>jakarta.persistence-api</artifactId>
            <version>3.2.0</version>
        </dependency>

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

EntityManagerFactory creates EntityManager. How to create EntityManagerFactory? - We can use a class to create EntityManagerFactory

We shouldnt be using DriverManagerDataSource in production as we need connection pool there. In our case, for every db operation, new connection is created. In realitime, we create connection
using ConnectionPool. DriverManagerDataSource doesnt return any connection pool. our application is simple henche using the DriverManagerDataSource.

In spring we have a class called LocalContainerEntityManagerFactoryBean which helps us create Entity mnagaer factory.

We dont have to create Entitymanager by ourself. We cannot autowire EntityManager(we can do but on special cases. We need to use SpringDataJpa). How to inject EntityManager object then? To initialise it we need to use
special annotation @PersistenceContext

If we use PersistenceContext, we need to activate transaction. We need to configure TransactionManager. TransactionManager provides Transaction management facility to our application.
Why we are using JpaTransactionManager and not JtaTransactionManager? - Whenever we connect to one database, we go with JpaTransactionManager. In case of connecting to multiple databases, we use 
JtaTransactionManager.

We need to tell spring to EnableTransaction.

Note: ComponentScan wont scan Entities. We need to tell EntityManager where our Entities are present. For this, we can use entityManagerFactoryBean.setPackagesToScan("com.springjpa.entity");
Or there's an annotation that can be used to achieve the same.

SPRINGDATAJPA

Why cant we use autowired with EntityManager? - We can use using SpringDataJPA. We need to use a special annotation over DBConfig i.e. @EnableJpaRepositories

Now for different requirements, we would need to develop methods that can say fetch a particular student,, or maybe all students etc etc. Instead we can let our dao(StudentDAO) extend 
JPARespository
