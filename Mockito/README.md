## Overview:

* `@Mock` — tells Mockito to create a fake `UserRepository`
* `@InjectMocks` — injects that mock into `UserService`
* `@ExtendWith(MockitoExtension.class)` — integrates Mockito with JUnit 5
* `Mockito.when(...).thenReturn(...)` — defines mock behavior
* `Assertions.assertEquals(...)` — validates expected output
