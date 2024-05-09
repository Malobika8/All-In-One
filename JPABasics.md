# **Java Persistence Api**

It's a specification of Java. It is used to persist data between java object and relational database. It's a bridge between object oriented data model and the relational database system.
It's a collection of classes and methods to store data into the database.
<img width="887" alt="Screenshot 2024-05-09 at 10 40 36 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/0bdcbfbb-3a47-4977-a522-3f9fe526f3ab">
<img width="819" alt="Screenshot 2024-05-09 at 10 41 08 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/630a3620-d169-4800-86ae-f698f5c2ff56">
<img width="1010" alt="Screenshot 2024-05-09 at 10 41 35 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/e3811199-7994-4376-a236-040ce85dfb05">
* Entities: Entities are the persistence objects stored in the database.
* Entity Manager: It's an interface and manage the persistence operations on object. One entity manager instance can manage multiple entities.
* Entity Transaction: It's a one to one relationship with the entity manager. For each entity manager operation, there is an entity transaction instance.
* Entity Manager factory: It's a factory class of the entity manager. It creates and manages multiple entity manager instances.
* Persistence: It contains the starting method to obtain entity manager factory instances

# **Object Relational Mapping**

It's a functionality used to develop and maintain a relationship between an object and a relational database. This can be done mapping one object state to a database column. It can manage different operations. Hibernate orm is one of the major jpa implementation and a popular option.

<img width="807" alt="Screenshot 2024-05-09 at 10 49 48 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/f0285457-1f09-45a7-83e8-af6c88828126">
<img width="1007" alt="Screenshot 2024-05-09 at 10 50 04 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/2a17d8a4-94a9-43dd-8200-79a99ebcd96d">


There are two ways to map a classes
* **Using an xml configuration:** The orm.xml file needs to be located in the resources/META-INF folder.
  
  *Sample*
  
  <img width="940" alt="Screenshot 2024-05-09 at 10 10 19 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/f781bbdd-d61c-43a6-b1c8-74652e4cab70">
* **Using annotations:** There are different annotations that can be used to map a class as an entity
  Ex - @Entity, @Id, @Column, @OneToOne etc.

  *Sample*
  
  <img width="921" alt="Screenshot 2024-05-09 at 10 12 09 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/531968db-ff4b-4ca2-9f43-ca045376460a">

# **Persistence Unit**
The persistence.xml configuration file is used to configure a given JPA Persistence Unit. The Persistence Unit defines all the metadata required to bootstrap an EntityManagerFactory, like entity mappings, data source, and transaction settings, as well as JPA provider configuration properties.

The goal of the EntityManagerFactory is used to create EntityManager objects we can for entity state transitions.

So, the persistence.xml configuration file defines all the metadata we need in order to bootstrap a JPA EntityManagerFactory.

** JPA persistence XML file location:**
Traditionally, the persistence.xml is located in a META-INF folder that needs to reside in the root of the Java classpath. If you’re using Maven, you can store it in the resources folder, like this:

src/main/resources/META-INF/persistence.xml

*Sample*

<img width="938" alt="Screenshot 2024-05-09 at 10 14 59 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/47ad6d38-41e4-4ceb-a171-4bcdb3094629">

# **EntityManager to interact with the database**
<img width="982" alt="Screenshot 2024-05-09 at 10 15 53 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/0dffa562-d8ac-4b29-91eb-67c6ca99b7a1">

# **Miscellaneous**
<img width="1024" alt="Screenshot 2024-05-09 at 10 33 02 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/f9ac7e9a-6115-4972-b6c1-54fd01d2e838">
<img width="1003" alt="Screenshot 2024-05-09 at 10 35 22 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/c6dfe468-48ea-4417-925d-ff1cd2615af5">








