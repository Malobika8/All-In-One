### 1. What are the different ways to inject dependencies?

- Setter injection (use property tag in xml config)
- Constructor injection (use constructor-arg tag in xml config)

### 2. How can we implicitely inject an object dependency in xml config?

<bean id="heart" class="com.human.heart.Heart"></bean>
<bean id="human" class="com.human.Human" ref="heart"></bean>

### 3. What is autowiring?

Spring can automatically wire/inject the objects wherever required provided the bean is available.

### 4. What are the different ways to autowire in xml?

- ByName: The Human class should have "heart" ref declared of "Heart" class.

  <bean id="heart" class="com.human.heart.Heart"></bean>
  <bean id="human" class="com.human.Human" autowire="byName"></bean>

- ByType: The Human class should have a ref declared of "Heart" type.

  <bean id="heart" class="com.human.heart.Heart"></bean>
  <bean id="human" class="com.human.Human" autowire="byType"></bean>

- Constructor
- Setter

### 5. Can we autowire in any other way if we don't want to configure in xml?

We can use @Autowire annotation. We need to enable annotation context in xml. 

### 6. Can we use autowire over literals?

No. This can only be used with object references.

### 7. Where all can we put @Autowire annotation?

- Over Constructor
- Over Setter
- Over object references

### 8. With constructor/setter injection, autowiring is done based on what?

It first tries to resolve based on type and then based on name.

### 9. What if there are multiple beans with name type and same name?

We can use @Qualifier annotation to declare the default impl to be used.
