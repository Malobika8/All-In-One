INTRODUCTION

JDBC has list of api's which lets user interact with the database without having to know structured query language.
It bridges the gap between a java application and database. It was originally developed by Sun Microsystems, later acquired by Oracle. Oracle now develops and maintains the same.
JDBC mostly has interfaces so that can be utilized for various databases available. Depending on the databases are JDBC Drivers which have relevant implementation that are made
use of. JDBC takes care of the internal conversion so that data can be accessed/manipulated as required. 
For it to work, the drivers are to be present in the application's classpath.
The drivers are however developed and maintained by database vendors.
<img width="1107" alt="Screenshot 2024-04-28 at 1 12 03 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/8d61c4b7-3149-423f-b803-b49f091969e1">
Important Classes(Orange) and Interfaces(Blue):
<img width="800" alt="Screenshot 2024-04-28 at 1 26 07 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/fbb0ca96-15ee-4cf9-9909-9005f5e0016e">

Steps to connect with Database
- Install Driver and set in Classpath
- Load the Driver:
  1) Loads the Class in memory - Class.forName("com.mysql.jdbc.Driver_name") (mention entire package name) Once the class is loaded, all the static statements/blocks will be executed.
  2) Or Pass  the object to Drivermanager - DriverManager.registerDriver(com.mysql.jdbc.Driver_name()
- Create a connection

      Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/dbname","root","password") (Static method)
- Create query, Statement, PreparedStatement, CallableStatement
  E.g:

       String q = "Select * from Students";
       Statement smt = con.createStatement();
       ResultSet set = smt.executeQuery(q);
- Process the data:

      while(set.next()){
          int id = set.getInt("studentID");
          String name = set.getName("studentName");
          System.out.println("ID:"+id+", Name:"+name);
      }
- Close the connection: con.close();
