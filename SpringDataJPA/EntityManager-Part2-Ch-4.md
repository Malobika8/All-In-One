![Screenshot 2024-06-24 at 10 46 37 PM](https://github.com/Malobika8/All-In-One/assets/111234135/bbc437a0-f2d5-448f-acb7-6188cff78199)## It is not required to create EntityManager on our own. 

##### Why so?

This is because with our current setup/approach, we cannot Autowire EntityManager.

(It is possible but on special cases. In such cases, we are required to use *SpringDataJpa*).

But then if we don't, how will it create the Bean?

##### How to inject EntityManager object then?

    An EntityManager instance is associated with a persistence context. To initialize it, we need to use a special annotation named *@PersistenceContext*.
    A persistence context is a set of entity instances in which for any persistent entity identity, there is a unique entity instance. 
    Within the persistence context, the entity instances and their lifecycle are managed.

    Persistence Context is a place which contains different Entities. It takes the responsibility of persisting entities onto the Database.
   
<img width="1005" alt="Screenshot 2024-06-25 at 8 57 05 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d53af30e-d750-4608-a299-9600c4ae0a94">

Let's try to run the Application now.

#### Error
   
<img width="975" alt="Screenshot 2024-06-25 at 8 58 27 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/51a305ff-73e8-4f38-8559-8c16df89af9b">

Currently the PersistenceUnit Name is set to "default. Let's first change the Persistence Unit name.

<img width="961" alt="Screenshot 2024-06-25 at 9 00 59 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8b1d4c23-a18d-4f4e-9ff4-d32ef14e40d8">
<img width="927" alt="Screenshot 2024-06-25 at 9 02 24 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/47c00a76-a8b9-48c3-9a20-e648fd48380b">

Run the application and notice unit name in the error.

<img width="539" alt="Screenshot 2024-06-25 at 9 29 36 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/5dcfce7d-5f7f-4f09-a4a0-366b416c2aee">

Let's now look at the main error.

<img width="973" alt="Screenshot 2024-06-25 at 9 32 30 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/fed854e9-c4f1-410f-b832-62ea8b5d046c">
<img width="687" alt="Screenshot 2024-06-25 at 9 32 44 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7b63cc1b-d617-4261-ad93-392aacfc35f7">

We need to use *@Transactional*. 

<img width="847" alt="Screenshot 2024-06-24 at 10 36 31 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/946b71e5-a203-461c-ac49-ade208e54a4b">

This is because whenever we use @PersistenceContext, PersistenceContextType is set by default. The default type is PersistenceContextType.TRANSACTION.

<img width="844" alt="Screenshot 2024-06-25 at 10 22 51 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/1335f4ae-b76f-4a5e-918b-5b75d7962713">

This means if we use PersistenceContext or EntityManager, by default it uses PersistenceContextType.TRANSACTION which is why we need to 
activate the TransactionManager. So whenever we do "persist", the transaction begins from method statement 1 and commit happens after the last statement.

<img width="829" alt="Screenshot 2024-06-25 at 10 29 06 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/3dcd11db-6766-458b-a689-5be018f6687b">

<img width="969" alt="Screenshot 2024-06-25 at 10 34 24 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/74a473de-2dd7-4fc2-9ad7-4e492b7be7df">

Let's try to run the Application.

#### Error

Just by adding the annotation, the TransactionManager won't be setup automatically for us.

**We need to configure TransactionManager.**

----------------------
*TransactionManager is a software component that manages transactions in a database. It ensures that multiple database operations, known      as transactions, are executed as a single, all-or-nothing unit of work. This means that if one operation within the transaction fails,       the entire transaction is rolled back, and all previous changes are reverted. TransactionManagers are commonly used in distributed           systems, financial applications, and other scenarios where data consistency and reliability are critical. They provide features such as      atomicity, consistency, isolation, and durability (ACID) to ensure data integrity and maintain business logic.*

*TransactionManager provides Transaction management facility to our application.*

----------------------

TransactionManager is the Interface. We need to use an appropriate implementation for the same.

There are multiple implemenatations available.

<img width="957" alt="Screenshot 2024-06-24 at 10 37 14 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a5acd542-9acc-441c-aba6-77a0ced606e8">

We should use *JpaTransactionManager* for our Application.

---------------
##### Why are we using JpaTransactionManager and not JtaTransactionManager?

*JpaTransactionManager* can be used whenever we want to connect to a single Database. The JpaTransactionManager is a Spring Framework component that manages transactions for Java Persistence API (JPA) based data access objects (DAOs). It provides a way to declaratively define transactional behavior for JPA-based data access operations. The JpaTransactionManager is responsible for creating and committing transactions, as well as handling rollbacks in case of exceptions. 

In scenarios where it is required to connect to  multiple databases, *JtaTransactionManager* is preferred. This TransactionManager is appropriate for handling distributed transactions, i.e. transactions that span multiple resources, and for controlling transactions on application server resources (e.g. JDBC DataSources available in JNDI) in general.

JpaTransactionManager is appropriate for Applications that use a single JPA EntityManagerFactory for transactional data access. JTA (usually through JtaTransactionManager) is necessary for accessing multiple transactional resources within the same transaction.

----------------

<img width="1005" alt="Screenshot 2024-06-25 at 10 47 21 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ef20f719-90e9-4b9e-9291-c43cee0ea19c">

Let's run the Application.

#### Error

<img width="972" alt="Screenshot 2024-06-25 at 10 49 51 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9c003d73-cfb7-49f1-8b74-3cc2ac8b9e30">

##### What went wrong?

We created the bean for TransactionManager but we need to tell Spring to use the same. This can be done by enabling Transaction.

<img width="861" alt="Screenshot 2024-06-24 at 10 43 00 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/0d0db86c-c677-48f1-ab54-185f78587747">

Let's try to run the Application now.

<img width="704" alt="Screenshot 2024-06-24 at 10 46 21 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/386eadf7-25ba-4063-89a5-28784966b60a">

**SUCCESSFULLY INSERTED!!!**

<img width="769" alt="Screenshot 2024-06-24 at 10 46 37 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/cc71e1f5-3374-4fe3-9284-770dc380c27b">









