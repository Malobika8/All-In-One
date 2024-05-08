# **Hibernate Query Language**

Get and load fetches the data based on Id's or primary key. What about complex queries? We would need **HQL(Hibernate Query Language)** in that case.
* SQL: Select * from xyzTable;
* HQL: from xyzTable

<img width="1083" alt="Screenshot 2024-05-08 at 10 31 49 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/c086a6f8-1c6c-4aee-a698-d8b56f07d968">

For dynamic queries, a parameter can be passed and set using session's setParameter method.

<img width="1044" alt="Screenshot 2024-05-08 at 11 08 45 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/44e05be2-7b7f-4cb6-ab93-2df58757fc9f">
<img width="900" alt="Screenshot 2024-05-08 at 11 47 07 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/3ef8ea2c-2198-4ecb-864e-be54e0071739">
<img width="897" alt="Screenshot 2024-05-08 at 11 52 02 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/76436884-3ced-457d-92f2-7af39a41f41a">

# **Pagination**
6 entries exist for Citizen table
<img width="930" alt="Screenshot 2024-05-08 at 1 37 12 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/d807ac18-e0dc-4ccf-8967-afd4ab6163b7">

Set starting index and maximum no of results that can be fetched
<img width="1014" alt="Screenshot 2024-05-08 at 1 36 01 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/cf3486c8-2cb5-4ecc-92d1-5cd52bf6b5da">

Retrieved batchwise as per the configuration done using setMaxResult and setFirstResult
<img width="1314" alt="Screenshot 2024-05-08 at 1 39 17 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/9fbd36b5-d63a-44fe-b160-b3dddfc64026">

# **Native SQL Query**
<img width="931" alt="Screenshot 2024-05-08 at 2 54 58 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/84e25856-5ac3-47dd-a613-06a3655848c5">

# **Cascading**
Cascading is a feature in Hibernate, which is an object-relational mapping (ORM) tool used in Java to map Java classes to database tables. Cascading refers to the ability to automatically propagate the state of an entity (i.e., an instance of a mapped class) across associations between entities. For example, if you have a Customer entity that has a one-to-many relationship with an Order entity, you can define cascading to specify that when a customer is deleted, all of their orders should be deleted as well.

Cascading in Hibernate refers to the automatic persistence of related entities. When a change is made to an entity, such as an update or deletion, the changes can be cascaded to related entities as well. Cascading can be configured using annotations, such as @OneToMany(cascade = CascadeType.ALL), or through XML configuration files. It is important to use cascading carefully, as it can lead to unwanted changes being made to related entities if not configured properly.

Hibernate provides several types of cascade options that can be used to manage the relationships between entities. Here are the different cascade types in Hibernate:

* CascadeType.ALL: CascadeType.ALL is a cascading type in Hibernate that specifies that all state transitions (create, update, delete, and refresh) should be cascaded from the parent entity to the child entities.
When CascadeType.ALL is used, and any operation performed on the parent entity will be automatically propagated to all child entities. This means that if you persist, update, or delete a parent entity, all child entities associated with it will also be persisted, updated, or deleted accordingly.
For example, consider a scenario where you have a Customer entity with a one-to-many relationship to Order entities. By using CascadeType.ALL, any operation performed on the Customer entity (such as persist, merge, remove, or refresh) will also be propagated to all associated Order entities.
Here’s an example of how CascadeType.ALL can be used:

      @OneToMany(mappedBy="customer", cascade=CascadeType.ALL) 
      private Set<Order> orders;

* CascadeType.PERSIST: CascadeType.PERSIST is a cascading type in Hibernate that specifies that the create (or persist) operation should be cascaded from the parent entity to the child entities.
When CascadeType.PERSIST is used, any new child entities associated with a parent entity will be automatically persisted when the parent entity is persisted. However, updates or deletions made to the parent entity will not be cascaded to the child entities.
For example, consider a scenario where you have a Customer entity with a one-to-many relationship to Order entities. By using CascadeType.PERSIST, any new Order entities associated with a Customer entity will be persisted when the Customer entity is persisted. However, if you update or delete a Customer entity, any associated Order entities will not be automatically updated or deleted.
Here’s an example of how CascadeType.PERSIST can be used:

      @OneToMany(mappedBy="customer", cascade=CascadeType.PERSIST) 
      private Set<Order> orders;
  
* CascadeType.MERGE: CascadeType.MERGE is a cascading type in Hibernate that specifies that the update (or merge) operation should be cascaded from the parent entity to the child entities.
When CascadeType.MERGE is used, any changes made to a detached parent entity (i.e., an entity that is not currently managed by the persistence context) will be automatically merged with its associated child entities when the parent entity is merged back into the persistence context. However, new child entities that are not already associated with the parent entity will not be automatically persisted.
For example, consider a scenario where you have a Customer entity with a one-to-many relationship to Order entities. By using CascadeType.MERGE, any changes made to a detached Customer entity (such as changes made in a different session or transaction) will be automatically merged with its associated Order entities when the Customer entity is merged back into the persistence context.
Here’s an example of how CascadeType.MERGE can be used:

      @OneToMany(mappedBy="customer", cascade=CascadeType.MERGE) 
      private Set<Order> orders;

* CascadeType.REMOVE: CascadeType.REMOVE is a cascading type in Hibernate that specifies that the delete operation should be cascaded from the parent entity to the child entities.
When CascadeType.REMOVE is used, any child entities associated with a parent entity will be automatically deleted when the parent entity is deleted. However, updates or modifications made to the parent entity will not be cascaded to the child entities.
For example, consider a scenario where you have a Customer entity with a one-to-many relationship to Order entities. By using CascadeType.REMOVE, any Order entities associated with a Customer entity will be automatically deleted when the Customer entity is deleted.
Here’s an example of how CascadeType.REMOVE can be used:

      @OneToMany(mappedBy="customer", cascade=CascadeType.REMOVE) 
      private Set<Order> orders;
  
* CascadeType.REFRESH: CascadeType.REFRESH is a cascading type in Hibernate that specifies that the refresh operation should be cascaded from the parent entity to the child entities.
When CascadeType.REFRESH is used, any child entities associated with a parent entity will be automatically refreshed when the parent entity is refreshed. This means that the latest state of the child entities will be loaded from the database and any changes made to the child entities will be discarded.
For example, consider a scenario where you have a Customer entity with a one-to-many relationship to Order entities. By using CascadeType.REFRESH, any associated Order entities will be automatically refreshed when the Customer entity is refreshed.
Here’s an example of how CascadeType.REFRESH can be used:

      @OneToMany(mappedBy="customer", cascade=CascadeType.REFRESH) 
      private Set<Order> orders;
  
* CascadeType.DETACH: CascadeType.DETACH is a cascading type in Hibernate that specifies that the detach operation should be cascaded from the parent entity to the child entities.
When CascadeType.DETACH is used, any child entities associated with a parent entity will be automatically detached when the parent entity is detached. This means that the child entities will become detached from the persistence context and their state will no longer be managed by Hibernate.
For example, consider a scenario where you have a Customer entity with a one-to-many relationship to Order entities. By using CascadeType.DETACH, any associated Order entities will be automatically detached when the Customer entity is detached.
Here’s an example of how CascadeType.DETACH can be used:

      @OneToMany(mappedBy="customer", cascade=CascadeType.DETACH) 
      private Set<Order> orders;
  
* CascadeType.REPLICATE: CascadeType.REPLICATE is a cascading type in Hibernate that specifies that the replicate operation should be cascaded from the parent entity to the child entities.
When CascadeType.REPLICATE is used, any child entities associated with a parent entity will be automatically replicated when the parent entity is replicated. This means that new child entities will be created and persisted in the database with the same state as the original child entities.
For example, consider a scenario where you have a Customer entity with a one-to-many relationship to Order entities. By using CascadeType.REPLICATE, any associated Order entities will be automatically replicated when the Customer entity is replicated.
Here’s an example of how CascadeType.REPLICATE can be used:

      @OneToMany(mappedBy="customer", cascade=CascadeType.REPLICATE) 
      private Set<Order> orders;
  
* CascadeType.SAVE_UPDATE: CascadeType.SAVE_UPDATE is a cascading type in Hibernate that specifies that the save or update operation should be cascaded from the parent entity to the child entities.
When CascadeType.SAVE_UPDATE is used, any child entities associated with a parent entity will be automatically saved or updated when the parent entity is saved or updated. This means that any changes made to the child entities will be persisted in the database along with the parent entity.
For example, consider a scenario where you have a Customer entity with a one-to-many relationship to Order entities. By using CascadeType.SAVE_UPDATE, any associated Order entities will be automatically saved or updated when the Customer entity is saved or updated.
Here’s an example of how CascadeType.SAVE_UPDATE can be used:

      @OneToMany(mappedBy="customer", cascade=CascadeType.SAVE_UPDATE) 
      private Set<Order> orders;

# **Caching in Hibernate**
<img width="1050" alt="Screenshot 2024-05-08 at 9 07 18 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/eec97aef-a95e-4c28-a9a2-a40c28dd045b">

First level caching is provided by default. Need configuration to enable second level caching.
<img width="1131" alt="Screenshot 2024-05-08 at 9 12 29 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/05943c2c-94ad-4e44-a388-b31f8145d438">

* **First level cache:** Session caches the data and persists till the session is closed. If a query is fired multiple times, it will hit     the database only once. Second time onwards, if the data is present in session cache and session is not closed, data will be fetched from
  session cache rather than hitting the database again.

  <img width="875" alt="Screenshot 2024-05-08 at 9 16 01 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/fb51151b-3def-4cdb-ac17-c8d5f8452f6d">
  <img width="870" alt="Screenshot 2024-05-08 at 9 16 34 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/e93eecdf-e912-4c1d-bb6c-08aa2bdf112d">

  To check if the object is present in Session cache, "contains" method can be used.
  
  <img width="631" alt="Screenshot 2024-05-08 at 9 21 32 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/d6ab07be-0307-4d48-a098-020d804a6372">

* **Second level cache:**
  - Add ehcache(cache implementation) dependency and add it to pom.xml.
  - Add hibernate ehcache and add it to pom.xml. Add the same version as hibernate-core.
    <img width="890" alt="Screenshot 2024-05-08 at 9 27 26 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/e8f76665-7154-4660-b449-7730262287d0">
  - Add property in configuration file and enable second level cache.
    <img width="746" alt="Screenshot 2024-05-08 at 9 29 30 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/7e35fc97-edc3-44fd-93ed-6b3acaccfd4a">
  - Add property and mention fully qualified ClassName
    <img width="956" alt="Screenshot 2024-05-08 at 9 52 10 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/a36156b2-17ba-4a65-af0f-fdd58eb9a430">
  - Add @Cacheable and @Cache annotations. Mention caching strategy.
    <img width="546" alt="Screenshot 2024-05-08 at 9 38 59 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/972b1bd4-db53-4695-891a-2e46d21bd53c">

  - SessionFactory now caches the object and to retrieve same object, it doesn't hit the database multiple times.
    <img width="931" alt="Screenshot 2024-05-08 at 9 52 59 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/87f2caf2-31f5-446e-a7bd-e1eeb1a988a8">
    <img width="874" alt="Screenshot 2024-05-08 at 9 55 34 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/22c55028-4907-4fea-bfa9-6196c14aac96">





  
