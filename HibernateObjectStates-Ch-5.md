# **Hibernate/Persistence Object States**
The Hibernate life cycle consists of four main states: Transient, Persistent, Detached, and Removed. Each of these states represents a specific state of an
object in the Hibernate framework.

<img width="1009" alt="Screenshot 2024-05-08 at 9 42 10 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/621d6fce-2e26-4d7f-8991-bb929fda46f4">
<img width="1057" alt="Screenshot 2024-05-08 at 9 52 25 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/94a60e12-d8b2-46d7-9697-06ae8a75f3e8">
<img width="947" alt="Screenshot 2024-05-08 at 9 54 16 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/c2de6a65-9224-4640-87f5-96843177b435">

1) **Transient State:** It refers to the state wherein there is an object created and its variables are initialized. When an object is created using the “new” keyword, it is in the
   transient state. The object is not associated with any Hibernate session, and no database operations are performed on it. The object is simply a plain Java object (POJO) that is
   not yet persisted in the database.

   **Code Sample**

       // Creating a new object in the transient state
       Employee employee = new Employee();
       employee.setName("John");
       employee.setAge(30);
   <img width="1062" alt="Screenshot 2024-05-08 at 10 08 46 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/52250ead-17bc-4408-9f2f-33934b9c54df">
   
3) **Persistence State:** It refers to the state wherein the objects gets associated to Session and later stored in Database in the form of tables.
   When an object is associated with a Hibernate session, it enters the persistent state. In this state, the object is associated with a specific Hibernate session and is actively
   managed by Hibernate. Any changes made to the object will be tracked by Hibernate and will be persisted to the database when the session is flushed.

   <img width="1067" alt="Screenshot 2024-05-08 at 10 13 43 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/266e459f-606c-472e-acb7-1ef30469d549">

   There are two sub-states of the persistent state: Transient-Persistent and Persistent-Detached.

   * Transient-Persistent State: When an object is first associated with a Hibernate session, it is in the Transient-Persistent state. This means that the object is newly created,
     and its state is not yet synchronized with the database. Any changes made to the object in this state will be persisted to the database when the session is flushed.

     **Code Example:**

          // Creating a new object in the Transient-Persistent state
          Employee employee = new Employee();
          employee.setName("John");
          employee.setAge(30); 

          // Associating the object with a Hibernate session
          Session session = HibernateUtil.getSessionFactory().openSession();
          session.beginTransaction();
          session.save(employee);
     
   * Persistent-Detached State: On the other hand, when an object is already in the database and is loaded into a Hibernate session, it is in the Persistent-Detached state.
      Any changes made to the object in this state will also be tracked by Hibernate and will be persisted to the database when the session is flushed.

      **Code Example:**

          // Loading an existing object into a Hibernate session
          Session session = HibernateUtil.getSessionFactory().openSession();
          Employee employee = session.get(Employee.class, 1L); 

          // Modifying the object in the Persistent-Detached state
          employee.setName("Alice"); 

          // Persisting the changes to the database
          session.beginTransaction();
          session.update(employee);
     
5) **Detached State:** It refers to the state when the object is dissociated with the Session post closure/clearance of Session. When a persistent object is no longer associated with
   a Hibernate session, it enters the detached state. This means that the object is no longer actively managed by Hibernate, and any changes made to it will not be persisted to the
   database. However, the object is still a valid Java object and can be re-associated with a Hibernate session in the future.

   <img width="1048" alt="Screenshot 2024-05-08 at 10 15 26 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/f187febe-6e15-47f3-aad3-af48c4b22b44">

   **Code Example:**

        // Loading an existing object into a Hibernate session
        Session session = HibernateUtil.getSessionFactory().openSession();
        Employee employee = session.get(Employee.class, 1L); 

        // Detaching the object from the Hibernate session
        session.evict(employee); 

        // Modifying the object in the Detached state
        employee.setAge(35); 

        // Re-associating the object with a Hibernate session
        session.beginTransaction();
        session.update(employee);
   
7) **Removed State:** It refers to the state when the object is deleted from the database. However, it may be available with the Session. When an object is deleted from the database,
   it enters the removed state. This means that the object is no longer associated with the database, and any attempts to modify it or re-associate it with a Hibernate session will
   result in an exception.

   **Code Example:**

        // Loading an existing object into a Hibernate session
        Session session = HibernateUtil.getSessionFactory().openSession();
        Employee employee = session.get(Employee.class, 1L); 

        // Deleting the object from the database and entering the Removed state
        session.beginTransaction();
        session.delete(employee);

   
