In Spring Data JPA, you can form queries in several ways. Here are the main approaches:

---

### 1. **Derived Query Methods**
Spring Data JPA can automatically derive the query from the method name.

**Example:**
```java
import org.springframework.data.jpa.repository.JpaRepository;

public interface UserRepository extends JpaRepository<User, Long> {
    // Find users by email
    User findByEmailId(String emailId);
    
    // Find users by name containing a substring
    List<User> findByNameContaining(String namePart);

    // Find users by age greater than a given value
    List<User> findByAgeGreaterThan(int age);
}
```

**Supported Keywords:**
- `And`, `Or`, `Between`, `LessThan`, `GreaterThan`, `Like`, `In`, `OrderBy`, etc.

---

### 2. **Custom JPQL Queries**
You can define JPQL queries using the `@Query` annotation.

**Example:**
```java
import org.springframework.data.jpa.repository.Query;
import org.springframework.data.repository.query.Param;
import org.springframework.stereotype.Repository;

@Repository
public interface UserRepository extends JpaRepository<User, Long> {
    @Query("SELECT u FROM User u WHERE u.emailId = :emailId")
    User findUserByEmail(@Param("emailId") String emailId);

    @Query("SELECT u FROM User u WHERE u.name LIKE %:namePart%")
    List<User> searchUsersByName(@Param("namePart") String namePart);
}
```

---

### 3. **Native SQL Queries**
For more complex or database-specific queries, you can use native SQL with the `@Query` annotation.

**Example:**
```java
@Repository
public interface UserRepository extends JpaRepository<User, Long> {
    @Query(value = "SELECT * FROM users WHERE email_id = :emailId", nativeQuery = true)
    User findUserByEmailNative(@Param("emailId") String emailId);
}
```

---

### 4. **Named Queries**
You can define queries directly in your entity class using the `@NamedQuery` annotation.

**Example:**
```java
import jakarta.persistence.*;

@Entity
@NamedQuery(name = "User.findByEmail", query = "SELECT u FROM User u WHERE u.emailId = :emailId")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(unique = true)
    private String emailId;

    private String name;
}
```

Repository usage:
```java
User user = userRepository.findByEmail("example@example.com");
```

---

### 5. **Criteria API (Dynamic Queries)**
Use the Criteria API for dynamically building queries in Java code.

**Example:**
```java
import jakarta.persistence.criteria.*;
import org.springframework.stereotype.Repository;
import org.springframework.beans.factory.annotation.Autowired;
import jakarta.persistence.EntityManager;

@Repository
public class UserCriteriaRepository {
    @Autowired
    private EntityManager entityManager;

    public List<User> findUsersByName(String namePart) {
        CriteriaBuilder cb = entityManager.getCriteriaBuilder();
        CriteriaQuery<User> query = cb.createQuery(User.class);
        Root<User> user = query.from(User.class);

        Predicate nameLike = cb.like(user.get("name"), "%" + namePart + "%");
        query.where(nameLike);

        return entityManager.createQuery(query).getResultList();
    }
}
```

---

### Which to Use?
- **Derived Queries**: Simple and quick for basic operations.
- **JPQL/Native Queries**: When custom queries are required.
- **Named Queries**: If the same query is used repeatedly.
- **Criteria API**: For complex dynamic queries. 

# Please read

https://docs.spring.io/spring-data/jpa/reference/jpa/query-methods.html

<img width="893" alt="Screenshot 2025-01-26 at 11 34 33 AM" src="https://github.com/user-attachments/assets/82856542-da92-4199-9b1b-7a6bb139989f" />
