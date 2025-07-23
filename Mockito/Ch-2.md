## 🎯 Goal: Use `@Mock` and `@InjectMocks` for cleaner tests

Instead of manually calling `mock()` and wiring everything, Mockito can do it for you automatically with:

### ✅ Annotations

| Annotation     | Purpose                                                     |
| -------------- | ----------------------------------------------------------- |
| `@Mock`        | Tells Mockito to create a mock object                       |
| `@InjectMocks` | Tells Mockito to inject the mocks into the class under test |

---

### ✅ Before vs After

#### ❌ Manual Way (what you did):

```java
UserRepository repository = Mockito.mock(UserRepository.class);
UserService service = new UserService(repository);
```

#### ✅ Cleaner Way:

```java
@Mock
UserRepository repository;

@InjectMocks
UserService service;
```

Mockito will **inject the mock automatically** into `UserService`.

---

## ✅ Full Example Using Annotations

```java
import com.random.repository.UserRepository;
import com.random.service.UserService;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.junit.jupiter.MockitoExtension;

import static org.mockito.Mockito.when;
import static org.junit.jupiter.api.Assertions.assertEquals;

@ExtendWith(MockitoExtension.class)
public class UserServiceTest {

    @Mock
    UserRepository repository;

    @InjectMocks
    UserService service;

    @Test
    public void getUserDisplayNameTest() {
        when(repository.findUserNameById(1)).thenReturn("Alice");
        assertEquals("User: Alice", service.getUserDisplayName(1));
    }
}
```

---

### ✅ Benefits:

* Cleaner test code
* No need to manually call `mock(...)`
* Mockito handles all wiring for you
* Easier to add more mocks later

---

## ✅ Bonus: Add `verify()` (optional but powerful)

To verify that the mock method was actually called:

```java
import static org.mockito.Mockito.verify;

@Test
public void getUserDisplayNameTest(){
    Mockito.when(repository.findUserNameById(1)).thenReturn("Alice");
    Assertions.assertEquals("User: Alice", userService.getUserDisplayName(1));

    // ✅ This checks that findUserNameById(1) was called exactly once
    verify(repository).findUserNameById(1);
}
```

---

