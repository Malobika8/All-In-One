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

