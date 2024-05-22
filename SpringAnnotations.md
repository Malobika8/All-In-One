# **Spring Annotations**

1. *@Component:* Creates an object for us and registers that object in the IOC container. @Component annotation can be used instead of       
  specifying beans in xml file. Similar to how an id was added in xml file to each bean, an id can be added to each component.

   <img width="722" alt="Screenshot 2024-05-22 at 7 21 41 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/af1662ac-ba86-4903-be21-3000c4d5c398">

   However, if an id is not mentioned, the class name will be considered as bean id.
  
   Make sure to enable Component Scan.

   <img width="842" alt="Screenshot 2024-05-22 at 7 48 55 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/fb6e559e-2e19-43a0-8582-a5ce134e5df9">

   <img width="1155" alt="Screenshot 2024-05-22 at 7 51 20 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/19ff8fb4-826e-47c3-be54-797c14889137">

2. *@Configuration:*  **What if we don't want to configure anything using xml file?**

  We can create a Config class using @Configuration annotation.

3. *@ComponentScan:* We can enable component scan using this annotation.

   <img width="1033" alt="Screenshot 2024-05-22 at 7 57 32 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/aa6e7de3-c678-4fb5-b599-dcbc49dcee6c">

   In that case, we need to make use of AnnotationConfigApplicationContext class and mention our newly created Config class.

   <img width="1039" alt="Screenshot 2024-05-22 at 8 01 50 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/ca5bcf80-3685-4fdb-854e-17ca036d3778">

4. *@Bean:* There's another way to create a bean. A method can be created in the Config class, method name being the bean id, which return 
   the
   object. For Spring to recognise method name as the bean id, @Bean annotation should be used.

   <img width="703" alt="Screenshot 2024-05-22 at 8 11 26 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/3df91297-313d-4020-97c4-5addc4784938">

   The bean name can be overriden as well.

   <img width="725" alt="Screenshot 2024-05-22 at 8 14 17 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/e5d98c5b-0735-4fe1-96bd-5f7b816dba01">
   <img width="735" alt="Screenshot 2024-05-22 at 8 16 25 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/512e9caa-e203-410c-bb61-36d38178c120">

   When there's a dependency, it can be injected as

   * Constructor injection:
    
     <img width="743" alt="Screenshot 2024-05-22 at 8 28 28 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/2cd5e450-7b57-4650-a5f9-a05222cef8dc">
     <img width="734" alt="Screenshot 2024-05-22 at 8 27 42 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/1ed0cf6e-d470-455d-99a1-9ee99485ac0b">

   * Setter injection

     <img width="731" alt="Screenshot 2024-05-22 at 8 33 04 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/0a7393b6-f582-41ff-85ad-52d25cd5d6b7">
     <img width="739" alt="Screenshot 2024-05-22 at 8 33 43 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/929c7033-533a-4ae8-9825-ac69181057e2">

5. *@Autowired:* For dependency injection.
6. *@Primary:* This can be used to declare one implementation as the primary implementation.

   <img width="742" alt="Screenshot 2024-05-22 at 9 35 56 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/ab8e38e3-c9c5-4115-a158-84c49c4d3890">

7. *@Qualifier:* In case of multiple implementation classes(for an interface), this annotation can be used to specify preferred 
   implementation.

   <img width="513" alt="Screenshot 2024-05-22 at 9 37 39 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/3f8d5da0-3745-471b-ab19-3957b37edf19">

   However, to avoid hard coding, we can create a properties file and load the implementation based on the implementation specified   on it.

# **Injecting literal values from properties file using Spring annotations**

* Create a properties file

  <img width="789" alt="Screenshot 2024-05-21 at 11 09 23 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/0dd93134-e7d7-4c74-856f-bee75be38224">
  <img width="1029" alt="Screenshot 2024-05-21 at 11 15 29 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/18cdb9f4-d493-49e9-8385-23f6a1655809">
  <img width="824" alt="Screenshot 2024-05-21 at 11 12 23 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/d70e7ba9-4342-437e-8c12-3f3845da3e54">

**But what if we don't want to set properties through xml file? - We can use annotations.**

8. *@Value:*

   <img width="1033" alt="Screenshot 2024-05-21 at 11 21 50 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/89379d1b-3b88-4887-a008-12413c958708">
   <img width="1126" alt="Screenshot 2024-05-21 at 11 21 59 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/748dcbb0-4f05-4803-86cb-e00b9d7f8b9f">

   This can be done by using @PropertySources annotation as well if we dont want to configure using xml.
  
   <img width="951" alt="Screenshot 2024-05-22 at 9 30 24 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/2eb87138-2208-4555-bd41-f52cac28949f">

   But which properties are mandatory? It we don't set any of the peroperty values, the value returned will be null. But a property can be     mandated using @Require annotation.

   <img width="1026" alt="Screenshot 2024-05-21 at 11 26 00 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/161b9ff2-7867-4211-9596-28a5b5b08da8">
   <img width="475" alt="Screenshot 2024-05-21 at 11 26 45 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/1535104a-1ba6-44c3-bee2-a51f06cf1560">

9. *@Require:*
  
   <img width="773" alt="Screenshot 2024-05-21 at 11 28 45 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/6a2c44a8-17e7-4ac9-a047-da9300eefa5b">

*Note: We can set from properties file as well.*

<img width="781" alt="Screenshot 2024-05-21 at 11 32 07 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/0b7c834e-b1fc-477f-85fc-8ce47ddfad14">

@Value can be placed diretly above the fields. In that case, setter methods are not made use of.

<img width="709" alt="Screenshot 2024-05-21 at 11 38 25 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/eda6043e-1cd4-4526-9b22-71d1d72626f1">

*Note: @Require can only be used above setter method and cant be used with fields directly.* 

<img width="723" alt="Screenshot 2024-05-22 at 9 43 59 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/4e3b2ca7-7765-4bbb-8d60-ce69a1c950fb">









  


