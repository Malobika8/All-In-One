  Classes need to be mapped to database tables. This can be done either using xml or annotation.
  # **Using annotation:**
  * @Entity: Marks the class as an entity. Hibernate will be able to save its object and fetch data.
  * @Id: Treats it as a primary key.
  * A property, Mapping, needs to be added in xml config file with fully qualified classname

        <mapping class="com.test.Student"/>

  **Sample code to create a table and insert data**
     
         //file path of hibernate.cfg.xml should be added in configure() if it's not auto-detected
         SessionFactory sessionFactory = new Configuration().configure("hibernate.cfg.xml").buildSessionFactory();
         System.out.println(sessionFactory);

         Student student = new Student();
         student.setId(102);
         student.setCity("Chakradharpur");
         student.setName("Malobika");

         Session session = sessionFactory.openSession();
         Transaction tx = session.beginTransaction();
         session.persist(student);
         tx.commit();
         session.close();

  We could see the sql queries successfully executed.
  <img width="1250" alt="Screenshot 2024-05-06 at 10 12 14 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/fce97a73-17b6-4fb9-a944-0ac1e0e806cf">
  <img width="518" alt="Screenshot 2024-05-06 at 10 14 34 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/85f70639-3cb6-4a67-be1d-fa567c2fd21a">

  # **Commonly used Hibernate annotations**
  - @Entity: Used to mark any class as Entity
  - @Table: Used to change table details
  - @Id: Used to mark column as Id(Primary Key)
  - @GeneratedValue: Hibernate will automatically generate values using an internal sequence. Therefore, we don't have to set it manually. For ex: If we want primary key to be generated
    automatically using a Strategy like AUTO_INCREMENT
  - @Column: Can be used to specify column mappings. For ex, to change the column name in the associated table in database.
  - @Transient: This tells hibernate not to save this file
  - @Temporal: Temporal over a data field tells hibernate the format in which the date needs to be saved.
  - @Lob: Lob tells hibernate that this is a large object not a simple object.
  - @OneToOne, @OneToMany, @ManyToOne, @JoinColumn etc.
 
  **Sample Code**

      class ...{
      @Entity
      @Table(name = "Student_Address")
      public class Address {
      @Id
      @GeneratedValue(strategy = GenerationType.IDENTITY)
      @Column(name = "address_id")
      private int addressId;
  
      @Column(length = 50)
      private String street;
  
      @Column(length = 100)
      private String city;
  
      @Column(name = "is_open")
      private boolean isOpen;
  
      @Transient
      private double x;
  
      @Column(name = "Date")
      @Temporal(TemporalType.DATE)
      private Date date;
  
      @Column(columnDefinition = "mediumblob")
      private byte[] image;
  
      ...}
      }

      public class Main {
        public static void main(String[] args) {
  
        System.out.println("Project started..");
        try{
            //file path of hibernate.cfg.xml should be added in configure() if it's not auto-detected
            SessionFactory sessionFactory = new Configuration().configure("hibernate.cfg.xml").buildSessionFactory();
            System.out.println(sessionFactory);

            //create Student object
            Student student = new Student();
            student.setId(102);
            student.setCity("Chakradharpur");
            student.setName("Malobika");

            //create Address object
            Address address=new Address();
            address.setStreet("Street1");
            address.setCity("Delhi");
            address.setOpen(true);
            address.setDate(new Date());
            address.setX(1234.123);
            //read image
            FileInputStream fis = new FileInputStream("src/main/resources/test.png");
            byte data[] = new byte[fis.available()];
            fis.read(data);
            address.setImage(data);

            Session session = sessionFactory.openSession();
            Transaction tx = session.beginTransaction();
            session.persist(student);
            session.persist(address);
            tx.commit();
            session.close();
        }
        catch(Exception e){
            e.printStackTrace();
        }

        System.out.println("Done..");
        }
      }

  Table created and data inserted

  <img width="452" alt="Screenshot 2024-05-06 at 11 18 16 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/13eb1ab5-b90e-42fd-bf1c-bc50b8257eff">

  # **Fetching Objects**

  There are two session methods that can be utilized to fetch objects.

  1) Get: It returns **null** if an object doesn't exist in the database. The fetched object is stored in the session cache which is utilized later. For fetch requests, it first checks
          the session cache and if not found, it hits the database.
          **Sample Code**

          public class FetchDemo {
           public static void main(String[] args) {

            Configuration cfg = new Configuration().configure("hibernate.cfg.xml");
            SessionFactory sessionFactory = cfg.buildSessionFactory();
            Session session = sessionFactory.openSession();

            //get (returns null if object not found)
            Student studentUsingGet = session.get(Student.class,102);
            System.out.println(studentUsingGet);

            session.close();
            sessionFactory.close();
            }
          }

     <img width="1207" alt="Screenshot 2024-05-07 at 11 30 56 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/ae47cf14-a673-45b7-9b3f-eb36b0ee1092">

     When Student object is requested twice, it fetches from session cache the second time.
     We could see the select statement being executed only once.

     <img width="1098" alt="Screenshot 2024-05-07 at 11 32 45 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/ac6388de-4a01-4690-aa70-bbedc9085ecd">

     Even when object details are not used, it fires a select query if not available in session cache.

         Configuration cfg = new Configuration().configure("hibernate.cfg.xml");
         SessionFactory sessionFactory = cfg.buildSessionFactory();
         Session session = sessionFactory.openSession();
         Student studentUsingGet = session.get(Student.class,102);
         session.close();
         sessionFactory.close();

     <img width="1160" alt="Screenshot 2024-05-07 at 11 41 38 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/1f85f341-4c91-4ba6-b9e1-63508c09bf35">
     
  2) Load: It returns **ObjectNotFoundException** if an object doesn't exist in the database. It does lazy initialization i.e. sends a proxy object initially. When some other data is
          is requested, only then it hits the database.
          **Sample Code**

          public class FetchDemo {
            public static void main(String[] args) {

              Configuration cfg = new Configuration().configure("hibernate.cfg.xml");
              SessionFactory sessionFactory = cfg.buildSessionFactory();
              Session session = sessionFactory.openSession();

              //load (returns ObjectNotFoundException if object not found)
              Student studentUsingLoad = session.load(Student.class,103);
              System.out.println(studentUsingLoad);

              session.close();
              sessionFactory.close();
             }
          }

     <img width="1029" alt="Screenshot 2024-05-07 at 11 31 36 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/a9cf1df6-87e2-4bee-a82d-f1ed642d8847">

     When Student object is requested, it simply returns a proxy object. It doesn't fire a select query until we try to use the object details in some way.

             Configuration cfg = new Configuration().configure("hibernate.cfg.xml");
             SessionFactory sessionFactory = cfg.buildSessionFactory();
             Session session = sessionFactory.openSession();
             Student studentUsingLoad = session.load(Student.class,103);
             session.close();
             sessionFactory.close();

     <img width="1336" alt="Screenshot 2024-05-07 at 11 43 13 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b01928d6-81f8-4ee7-b32a-39c9726c09bd">

     <img width="1014" alt="Screenshot 2024-05-07 at 10 53 02 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/57002a79-e325-4271-b3da-0719145b3a48">

   # **Embedding Objects**

   JPA provides the @Embeddable annotation to declare that a class will be embedded by other entities.

   <img width="1129" alt="Screenshot 2024-05-07 at 11 47 33 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/fd01d5f7-812c-4412-ae68-1b1426a9f6cf">

   Without @Embedabble annotation, it complains of JdbcTypeRecommendationException.

   <img width="1332" alt="Screenshot 2024-05-07 at 12 13 17 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/ee2d38aa-1718-469c-9cdc-c1ef79e34288">

   With @Embeddable annotation, it works as expected.

   <img width="415" alt="Screenshot 2024-05-07 at 12 16 39 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/1e928c11-a671-4a68-8614-14ef60025b0e">

   Ex. If Certificate is embedded onto Student, the Certificate columns(course, duration) are added as well.

   <img width="1343" alt="Screenshot 2024-05-07 at 12 17 38 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/5362c5ea-e756-4d49-920f-e9c312d38534">
   <img width="416" alt="Screenshot 2024-05-07 at 12 20 32 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/f03286f5-940d-4ccb-abee-391e8371feaa">

   # **OneToOneMapping**
   <img width="1122" alt="Screenshot 2024-05-07 at 12 34 40 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/08948100-ed2f-477b-a649-7bd337b14a3f">
   <img width="1082" alt="Screenshot 2024-05-07 at 12 37 29 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/8c71f317-a03d-41b5-9c4d-1870746a66be">
   <img width="881" alt="Screenshot 2024-05-07 at 1 00 27 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/12dbe2e8-47db-493e-9a4d-db3b84826d0f">
   <img width="953" alt="Screenshot 2024-05-07 at 1 07 58 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/3ba88019-9f89-4839-a310-ffe20c93bf0c">
   <img width="1267" alt="Screenshot 2024-05-07 at 1 09 52 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/6129dcd1-826d-4651-9145-e6972e67f6b9">
   <img width="1279" alt="Screenshot 2024-05-07 at 1 10 19 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/77068fdd-1584-4539-b046-f4c744f7c4b5">
   <img width="953" alt="Screenshot 2024-05-07 at 1 07 58 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/9f227f2c-d7de-4348-9f75-ed4121d67b59">
   <img width="765" alt="Screenshot 2024-05-07 at 1 10 57 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/7efbe8ec-4c96-4366-b2a8-43c03bf2043d">
   <img width="808" alt="Screenshot 2024-05-07 at 1 11 10 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/f5fd5835-bac1-4dfb-b164-3b9d4ea37b2c">
   
   In case of Bidirectional mapping,
   
   <img width="886" alt="Screenshot 2024-05-07 at 10 10 14 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b881bd24-2405-429d-8bac-f0be6c1ae6f9">

   Foreign key column can be renamed by using @JoinColumn annotation
   <img width="861" alt="Screenshot 2024-05-07 at 1 12 32 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/1b88b3c3-4f8c-4055-964b-8725f55a110b">

   # **OneToManyMapping**
   
   <img width="875" alt="Screenshot 2024-05-07 at 10 42 05 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/db23fbcc-cdf5-4e64-879f-52f8367e8e6b">
   <img width="896" alt="Screenshot 2024-05-07 at 10 42 14 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/3e1b7852-335c-42a3-a124-5229b5b138a4">
   <img width="1309" alt="Screenshot 2024-05-07 at 10 42 38 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/f9996215-fa14-4358-a765-f769709f6915">
   <img width="1261" alt="Screenshot 2024-05-07 at 10 44 59 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/5d609055-e0fb-426a-a169-e1905a815e79">
   <img width="872" alt="Screenshot 2024-05-07 at 10 45 26 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/745dfed7-b79f-4215-a425-37bf2d86e16a">
   <img width="929" alt="Screenshot 2024-05-07 at 10 45 42 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/519f2d25-fff6-4cbb-b564-79bc7f98eb74">

   # **ManyToMany**
   <img width="935" alt="Screenshot 2024-05-07 at 11 22 54 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b8f03ccb-7919-4cdd-ab13-33b71c9259cf">
   <img width="1035" alt="Screenshot 2024-05-07 at 11 23 14 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/e099b614-a18d-426b-bd18-aa24d4fa1756">
   <img width="1195" alt="Screenshot 2024-05-07 at 11 23 33 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/1be59101-e079-4a4d-920b-bc357f24e945">
   <img width="1228" alt="Screenshot 2024-05-07 at 11 25 14 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b1ac018c-1269-492e-b869-253cca608f75">
   <img width="1170" alt="Screenshot 2024-05-07 at 11 25 01 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/20f27a6e-12a7-4c5b-a7e2-1ba6586fab15">
   <img width="852" alt="Screenshot 2024-05-07 at 11 26 31 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/878e997c-b582-418d-aa4f-243d269a0d98">
   <img width="881" alt="Screenshot 2024-05-07 at 11 26 43 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/fa772386-5da6-4858-b823-9a8d0dae35ca">
   <img width="898" alt="Screenshot 2024-05-07 at 11 26 54 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/5a36f98a-d4dd-4131-a769-851a8e409ea3">



















  
