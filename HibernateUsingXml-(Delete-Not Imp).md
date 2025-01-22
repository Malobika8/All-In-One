# **Using XML mapping**

<img width="1134" alt="Screenshot 2024-05-08 at 10 23 09 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/294a6749-43b4-49a8-87c8-3efe5fa33695">

Person entity

<img width="851" alt="Screenshot 2024-05-08 at 10 26 29 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b15d459d-20d5-4b5c-b24f-14dd65da9310">

Entity mapping (Filename: Person.hbm.xml)

<img width="924" alt="Screenshot 2024-05-08 at 10 29 05 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/2c9b2043-6689-4d71-92d6-542ba1732f1b">

hibernate.cfg.xml

<img width="922" alt="Screenshot 2024-05-08 at 10 30 14 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/4becbf39-2427-4db8-9f9b-672807153338">
<img width="936" alt="Screenshot 2024-05-08 at 10 31 52 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/e940554b-926b-471e-8288-33e0d11c9c0c">
<img width="884" alt="Screenshot 2024-05-08 at 10 32 39 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/1d2c10a8-d340-4a68-9f50-12e36870e9bc">

# Important

In the context of Hibernate, **HBM** stands for **Hibernate Mapping**. It refers to the XML-based mapping files (with `.hbm.xml` extension) used to define the mapping between Java objects (entities) and database tables. 

The term **hbmddl** is commonly associated with the Hibernate **hbm2ddl** tool. Here's what the components mean:

- **HBM**: Hibernate Mapping, which specifies the mappings between your Java objects and the database.
- **DDL**: Data Definition Language, which refers to SQL commands like `CREATE`, `ALTER`, and `DROP` that define or modify database schema.

### hbm2ddl in Hibernate
The `hbm2ddl` tool is used to automatically generate or update the database schema based on the mappings defined in `.hbm.xml` files or annotations. It helps developers avoid writing SQL schema scripts manually.

### Common `hbm2ddl` Configuration Values
In Hibernate, `hibernate.hbm2ddl.auto` is a configuration property that controls the behavior of schema generation. Some common values include:

- `validate`: Validates the schema against the mappings.
- `update`: Updates the schema without destroying existing data.
- `create`: Creates the schema, dropping existing data.
- `create-drop`: Creates the schema and drops it when the session ends.
- `none`: No action is performed.

### Modern Hibernate Usage
While `.hbm.xml` files are still supported, most modern Hibernate projects prefer using **JPA annotations** for mapping because they are more concise and integrate seamlessly with Java code.
