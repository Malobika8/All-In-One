### 1. What do you mean by Spring IOC?

Earlier, we were responsible for creating objects for classes. 

Spring is now responsible for creating and managing the objects. As the name suggests, IOC (i.e. inversion of control) means the control lies with Spring rather than users.

### 2. What are the types of IOC containers available?

- BeanFactory
- ApplicationContext (Latest with more features)

Both of these are interfaces.
  
### 3. What do you mean by Spring beans?

The objects created by Spring in the IOC container are referred to as Spring beans.

### 4. How to create Spring beans with XML config

```
<bean id="someId" class="com.class.sampleclass"> </bean>
```

### 5. How many ways can dependency injection be done?

- Setter Injection (we can use the "property" tag for setter injection)
- Constructor Injection (we can use the "constructor-arg" tag for constructor injection)

Dependencies can be in the form of:
- Literals
- Objects
- Collection

### 6. How to inject literals through XML config using setter & constructor injection?

- Setter injection: (Note that providing "type" is optional as Spring resolves the type by itself.

  ```
  <bean id="someId" class="com.class.sampleclass">
    <property name="uniqueNo" value="2" type="int" />
    <property name="uniqueName" value="Sample Name" type="java.lang.String" />
  </bean>

- Constructor injection: (Note that providing "type" is optional as Spring resolves the type by itself.

  ```
  <bean id="someId" class="com.class.sampleclass">
    <constructor-arg name="uniqueNo" value="2" type="int" />
    <constructor-arg name="uniqueName" value="Sample Name" type="java.lang.String" />
  </bean>

### 7. How do you inject objects through XML config using setter & constructor injection?

<img width="634" alt="Screenshot 2024-09-16 at 10 47 38 AM" src="https://github.com/user-attachments/assets/e0cfe64e-bce3-4ff0-ab74-586524fefd08">

A better way is to create a bean separately & reference it wherever required.

<img width="1155" alt="Screenshot 2024-09-16 at 11 20 38 AM" src="https://github.com/user-attachments/assets/8ffa9897-0424-46d9-af27-e4d96a077848">
<img width="1013" alt="Screenshot 2024-09-16 at 11 19 31 AM" src="https://github.com/user-attachments/assets/935c20e5-a522-42bb-bd21-a55b94b81625">













