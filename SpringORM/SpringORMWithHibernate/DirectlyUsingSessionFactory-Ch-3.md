You can absolutely do everything without `HibernateTemplate`. In fact, Spring provides a more flexible and modern way to interact with Hibernate through **`SessionFactory`** and **`Session`** directly. The `HibernateTemplate` is an older approach that abstracts much of the Hibernate functionality and was commonly used in older versions of Spring. With modern Spring versions, it's common to work directly with the `SessionFactory` and `Session` objects, or to use the `JpaRepository` for JPA-based operations.

Here’s how you can proceed without `HibernateTemplate`:

### Steps to Use Hibernate Without `HibernateTemplate`

1. **Remove `HibernateTemplate`** from your configuration:
   - You don’t need it anymore if you are directly using `SessionFactory` and `Session`.

2. **Use `SessionFactory` and `Session` directly**:
   - `SessionFactory` provides a way to open a `Session`, which is where you perform the actual database operations like `save()`, `update()`, `delete()`, etc.

3. **Transaction Management**:
   - You can still use Spring's `@Transactional` annotation to manage transactions.

### Example: Basic Hibernate Configuration Without `HibernateTemplate`

#### 1. Configuration Class
```java
@Configuration
@EnableTransactionManagement
public class AppConfig {

    public Properties hibernateProperties() {
        Properties properties = new Properties();
        properties.put("hibernate.show_sql", true);
        properties.put("hibernate.format_sql", true);
        properties.put("hibernate.hbm2ddl.auto", "update");

        return properties;
    }

    @Bean
    public DataSource dataSource() {
        DriverManagerDataSource dataSource = new DriverManagerDataSource();
        dataSource.setDriverClassName("com.mysql.cj.jdbc.Driver");
        dataSource.setUrl("jdbc:mysql://127.0.0.1:3306/DB1");
        dataSource.setUsername("root");
        dataSource.setPassword("password");

        return dataSource;
    }

    @Bean
    public SessionFactory sessionFactory() {
        LocalSessionFactoryBean sessionFactoryBean = new LocalSessionFactoryBean();
        sessionFactoryBean.setDataSource(dataSource());
        sessionFactoryBean.setHibernateProperties(hibernateProperties());
        sessionFactoryBean.setPackagesToScan("com.spring.orm.hibernate.entity");

        try {
            sessionFactoryBean.afterPropertiesSet(); // Initialize SessionFactory
        } catch (Exception e) {
            throw new RuntimeException("Error creating sessionFactory", e);
        }

        return sessionFactoryBean.getObject();
    }

    @Bean
    public HibernateTransactionManager hibernateTransactionManager() {
        HibernateTransactionManager hibernateTransactionManager = new HibernateTransactionManager(sessionFactory());
        return hibernateTransactionManager;
    }
}
```

#### 2. DAO Class Using `SessionFactory` and `Session`
```java
@Component
public class PersonDao {

    @Autowired
    private SessionFactory sessionFactory;

    @Transactional
    public void savePerson(Person person) {
        Session session = sessionFactory.getCurrentSession();
        session.save(person); // Directly using Hibernate's Session object
    }

    @Transactional
    public void updatePerson(Person person) {
        Session session = sessionFactory.getCurrentSession();
        session.update(person); // Directly using Hibernate's Session object
    }

    @Transactional
    public Person getPersonById(int id) {
        Session session = sessionFactory.getCurrentSession();
        return session.get(Person.class, id); // Directly using Hibernate's Session object
    }
}
```

#### 3. Main Application Class to Test
```java
@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
        PersonDao personDao = context.getBean(PersonDao.class);

        Person person = new Person();
        person.setName("John Doe");
        personDao.savePerson(person);

        Person retrievedPerson = personDao.getPersonById(person.getId());
        System.out.println(retrievedPerson.getName());
    }
}
```

### Explanation:

1. **SessionFactory**:
   - We still use the `SessionFactory` to create `Session` objects, which are used to interact with the database.
   - In the DAO class, we inject `SessionFactory` and obtain the current session by calling `sessionFactory.getCurrentSession()`.

2. **Transactional**:
   - The `@Transactional` annotation ensures that the operations are wrapped in a transaction context, and Spring will automatically manage the commit/rollback of the transaction.

3. **No `HibernateTemplate`**:
   - We directly call `session.save()`, `session.update()`, etc., using the Hibernate `Session` object.
   - This gives us more control over the Hibernate operations and is a more modern approach.

### Why Use This Approach:

- **Flexibility**: Directly using `SessionFactory` and `Session` gives you full control over Hibernate's features.
- **More Power**: You can access all Hibernate capabilities (like Criteria, native queries, etc.) without the limitations of `HibernateTemplate`.
- **Better Integration**: You can integrate seamlessly with Spring's declarative transaction management (`@Transactional`) and don’t need the abstraction that `HibernateTemplate` provides.
- **Modern**: This approach is more in line with modern Spring practices, where using `SessionFactory` and `Session` is standard.

### Conclusion:
You can definitely do everything without `HibernateTemplate`. By directly using `SessionFactory` and `Session`, you're working with the core Hibernate API, which gives you more flexibility and control.
