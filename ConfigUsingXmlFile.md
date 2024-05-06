# **Configuration using xml file**

1) Add an xml file named "hibernate.cfg.xml" in **src/main/resources** folder (**not in src/main/java**).

    <img width="636" alt="Screenshot 2024-05-02 at 10 46 21 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/0758c12b-5184-4ed2-8540-666d8de8de8a">

2) Add hibernate ddt:
 
       <!DOCTYPE hibernate-configuration PUBLIC
       "-//Hibernate/Hibernate Configuration DTD 3.0//EN"
       "http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">
  
3) Declare all the properties under "hibernate-configuration" -> "session-factory" tag.

       <hibernate-configuration>
        <session-factory>
        <!-- Driver class -->
        <property name="connection.driver_class">com.mysql.cj.jdbc.Driver</property>
        <!-- Connection url -->
        <property name="connection.url">jdbc:mysql://localhost:3333/DB1</property>
        <!-- Username -->
        <property name="connection.username">root</property>
        <!-- Password -->
        <property name="connection.password">password</property>
        <!-- Dialect as per the database -->
        <property name="dialect">org.hibernate.dialect.MySQLDialect</property>
        <!-- So that table is updated, if already exists, otherwise created -->
        <property name="hbm2ddl.auto">update</property>
        <!-- To show sequel queries -->
        <property name="show_sql">true</property>
        </session-factory>
       </hibernate-configuration>

4) Create an object of SessionFactory(Interface): Session Factory is a thread safe object that creates session which helps in saving objects/data.
 
          //file path of hibernate.cfg.xml should be added in configure() if it's not auto-detected
          SessionFactory sessionFactory = new Configuration().configure("hibernate.cfg.xml").buildSessionFactory();


