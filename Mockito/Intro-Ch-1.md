## 🎭 What is Mockito?

**Mockito** allows you to:

* **Mock** (fake) dependencies like repositories, services, or external APIs.
* **Focus on testing your class logic only**.
* **Avoid actual DB/API calls** in unit tests.

---

## ✅ Real-World Analogy

Imagine you're testing a **Service** class that calls a **Repository** (which hits a DB).

In a **unit test**, you don't want to hit the real DB — you just want to:

* Pretend (`mock`) that the repository behaves a certain way.
* Focus on testing your **Service** logic only.

---

## 📦 Add Mockito to Your Maven `pom.xml`

Add this:

```xml
<dependency>
  <groupId>org.mockito</groupId>
  <artifactId>mockito-core</artifactId>
  <version>5.12.0</version>
  <scope>test</scope>
</dependency>
```

Also, since you're using JUnit 5, add this too:

```xml
<dependency>
  <groupId>org.mockito</groupId>
  <artifactId>mockito-junit-jupiter</artifactId>
  <version>5.12.0</version>
  <scope>test</scope>
</dependency>
```

---

## ✅ Example: Service + Repository

### Step 1: Create the real classes

```java
// Real dependency
public interface UserRepository {
    String findUserNameById(int id);
}

// Class you want to test
public class UserService {
    private UserRepository repo;

    public UserService(UserRepository repo) {
        this.repo = repo;
    }

    public String getUserDisplayName(int id) {
        return "User: " + repo.findUserNameById(id);
    }
}
```

---

### Step 2: Write a unit test with Mockito

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.junit.jupiter.MockitoExtension;
import static org.mockito.Mockito.*;
import static org.junit.jupiter.api.Assertions.*;

@ExtendWith(MockitoExtension.class)
public class UserServiceTest {

    @Test
    void testGetUserDisplayName() {
        // Step 1: Create mock of the repository
        UserRepository mockRepo = mock(UserRepository.class);

        // Step 2: Define its behavior
        when(mockRepo.findUserNameById(1)).thenReturn("Alice");

        // Step 3: Inject the mock into the service
        UserService service = new UserService(mockRepo);

        // Step 4: Test the service method
        String result = service.getUserDisplayName(1);
        assertEquals("User: Alice", result);
    }
}
```

---

### ✅ Key Mockito Concepts:

| Concept                     | Example                                              | Meaning                     |
| --------------------------- | ---------------------------------------------------- | --------------------------- |
| `mock()`                    | `mock(UserRepository.class)`                         | Creates a fake object       |
| `when(...).thenReturn(...)` | `when(repo.findUserNameById(1)).thenReturn("Alice")` | Define fake behavior        |
| `verify()`                  | `verify(repo).findUserNameById(1)`                   | Verify interaction happened |

---

