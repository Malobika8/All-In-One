## 1. **What is the difference between `CrudRepository`, `JpaRepository`, and `PagingAndSortingRepository`? Which one do you prefer and why?**

### Sol:

#### Difference Between Repositories

| Interface                           | Inherits From                | Features                                                                   |
| ----------------------------------- | ---------------------------- | -------------------------------------------------------------------------- |
| `CrudRepository<T, ID>`             | -                            | Basic CRUD: `save()`, `findById()`, `findAll()`, `deleteById()`            |
| `PagingAndSortingRepository<T, ID>` | `CrudRepository`             | Adds `findAll(Sort sort)` and `findAll(Pageable pageable)`                 |
| `JpaRepository<T, ID>`              | `PagingAndSortingRepository` | Full-featured JPA support, batch operations, flush, `@Query` support, etc. |

#### 🔹 When to Use Which?

| Scenario                                          | Repository                             |
| ------------------------------------------------- | -------------------------------------- |
| Only basic CRUD needed                            | `CrudRepository`                       |
| Need pagination or sorting                        | `PagingAndSortingRepository`           |
| Advanced JPA usage, custom queries, batch inserts | `JpaRepository` ✅ (most commonly used) |

You can extend `JpaRepository`, and you get **everything** from all 3.

```java
public interface UserRepository extends JpaRepository<User, Long> {
    List<User> findByName(String name); // method name query
}
```

---

## 2. Create a JPA entity `User` with fields:

* `id` (Long, primary key)
* `name` (String)
* `email` (String, unique)

Create a `UserRepository` with a method to:

* Find all users by name

### Sol:

#### 1️⃣ `User` Entity

```java
import jakarta.persistence.*; // or javax.persistence.* for older versions
import lombok.*;

@Entity
@Getter
@Setter
@NoArgsConstructor
@AllArgsConstructor
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    @Column(unique = true)
    private String email;
}
```

#### 2️⃣ `UserRepository`

```java
import org.springframework.data.jpa.repository.JpaRepository;
import java.util.List;

public interface UserRepository extends JpaRepository<User, Long> {
    List<User> findByName(String name);
}
```

#### 3️⃣ Configuration (Not Required in Spring Boot)

If you're using **Spring Boot**, you don’t need a manual `AppConfig` class to enable JPA repositories unless you're customizing base packages.

But if you want to add it, here’s how:

```java
import org.springframework.context.annotation.Configuration;
import org.springframework.data.jpa.repository.config.EnableJpaRepositories;

@Configuration
@EnableJpaRepositories(basePackages = "com.example.repository")
public class AppConfig {
}
```


#### ✅ Summary

```
@Entity class User         ✅
@Repository interface UserRepository ✅
@SpringBootApplication or @Configuration ✅
```

---

## 3. **How does Spring Data JPA create queries from method names like `findByNameAndEmail()`? What are the limitations of this approach?**

### Sol:

#### How Spring Data JPA Derives Queries from Method Names

Spring Data JPA analyzes **method names** in repository interfaces and automatically generates queries using predefined **keywords** like:

| Keyword                                                           | Meaning            |
| ----------------------------------------------------------------- | ------------------ |
| `findBy`, `readBy`, `getBy`                                       | Start of the query |
| `And`, `Or`                                                       | Logical connectors |
| `Between`, `LessThan`, `GreaterThan`, `Like`, `IsNull`, `NotNull` | Conditions         |
| `OrderBy`                                                         | Sorting results    |

#### Example

```java
List<User> findByNameAndEmail(String name, String email);
```

Internally, Spring generates:

```sql
SELECT * FROM user WHERE name = ? AND email = ?
```

#### ❗ Limitations

- **Long method names** if too many fields:
   `findByNameAndEmailAndPhoneAndAge...` → not readable
- **No support for complex logic or joins**
- **Static queries only** — not dynamic

> For complex queries, prefer:

* `@Query` annotation (JPQL/SQL)
* `QueryDSL`, `Specifications`, or `EntityManager` for dynamic ones

---

## 4. Add to your `UserRepository`:

* A method using `@Query` to fetch a user by **email**
* The JPQL query should be:
  `SELECT u FROM User u WHERE u.email = :email`

Write only the repository interface code 👇

### Sol:

```java
import org.springframework.data.jpa.repository.Query;
import org.springframework.data.repository.query.Param;

public interface UserRepository extends JpaRepository<User, Long> {

    @Query("SELECT u FROM User u WHERE u.email = :email")
    User findUserByEmail(@Param("email") String email);
}
```

#### Notes:

* `@Query` lets you write **JPQL** or **native SQL**
* `:email` refers to a **named parameter**
* `@Param("email")` maps it to the method parameter

---

## 5. **What’s the difference between JPQL and native SQL in Spring Data JPA? When would you use each?**

### Sol:

#### JPQL vs Native SQL

| Feature     | JPQL (Java Persistence Query Language)            | Native SQL                                          |
| ----------- | ------------------------------------------------- | --------------------------------------------------- |
| Operates On | **Entities** and their fields (e.g., `User.name`) | **Database tables** and columns (e.g., `user.name`) |
| Portability | ✅ Database-independent                            | ❌ Tied to a specific DB                             |
| Syntax      | Similar to SQL but **object-oriented**            | Standard SQL                                        |
| Use Case    | Simple to medium queries on entities              | Complex queries, joins, DB-specific features        |
| Example     | `SELECT u FROM User u WHERE u.email = :email`     | `SELECT * FROM users WHERE email = ?`               |

#### 🔸 When to Use:

* Use **JPQL** when:

  * You want portability across databases
  * You're working with mapped entity fields
  * Query is relatively simple

* Use **Native SQL** when:

  * You need to use DB-specific functions (e.g., Postgres `ILIKE`, MySQL `REGEXP`)
  * Complex joins across unrelated tables
  * Performance tuning with DB indexes/hints

You can use native SQL like this:

```java
@Query(value = "SELECT * FROM users WHERE email = :email", nativeQuery = true)
User findByEmailNative(@Param("email") String email);
```

---



