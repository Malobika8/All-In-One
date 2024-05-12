# **Good to know info**
* Developer - Rod Johnson
* Org- spring org/pivotal
* Initial name - Interface 21 (later changed to Spring)

Spring has become an alternative technology in Java world for the EJB model. Spring is lightweight as compared to ejb's.
Why AWT's are heavy weight and not Swings? Because the AWT's uses OS libraries but not swings. Swings just use jdk libraries.
Similarly, for ejb's, application server is needed. In case of Spring, only spring jars and jdk is required.
We have different frameworks available for different needs like struts for web development, ejb for enterprise application & jpa for database. Spring handles all of it.

# **Spring Core**

Spring is one of the most widely used Java EE frameworks. It is famous because it solves one of the most important issue i.e. dependency. Spring Framework is based on two 
design principles - Dependency Injection and Aspect Oriented Programming.
Spring Framework is built on the Inversion of Control principle. Dependency injection is the technique to implement IoC in applications.

# **Spring Framework Architecture**
Spring Framework is divided into a number of separate modules, which allows you to decide which ones to use in your application. The below image illustrates the most important
modules of Spring Framework architecture.
<img width="694" alt="Screenshot 2024-05-10 at 11 42 27 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/0f9afd39-a48a-4aed-a092-bc3ba764b595">

**Use spring framework to get the object (Simple spring project)**
* Add spring context dependency
  <img width="798" alt="Screenshot 2024-05-10 at 11 49 03 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/11ae3706-426f-4d4e-bc04-b321b2a56084">
* Create a simple class
* Create an xml file and add configurations required for creating a bean(object of the class).
  <img width="962" alt="Screenshot 2024-05-10 at 11 53 26 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/c9d41f10-2276-498e-baee-f431db2315d7">
* Without creating an object of the class manually, we can get the bean using getBean method. This can be availed using Beanfactory(interface). To get a BeanFactory object, use a class
  that implements the same.
  <img width="902" alt="Screenshot 2024-05-10 at 11 53 15 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/9aaaacf2-0b97-467b-bede-1e1472d15b1a">

**Application Context**

Spring initially was mainly focused on Dependency injection. But later they started adding new features. For new features, new methods are required. Those methods are not available in
BeanFactory. So instead of BeanFactory, another interface can be used which is ApplicationContext.

<img width="873" alt="Screenshot 2024-05-11 at 12 05 47 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/a980eebe-04a7-4385-910e-0c0f8c0e02f0">

**Spring Container**

Even if we don't immediately use the object, spring creates and keeps the object ready to be injected at any point of time. 

<img width="544" alt="Screenshot 2024-05-11 at 12 11 18 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/2a992fdb-e730-4550-a023-689858925a93">
<img width="935" alt="Screenshot 2024-05-11 at 12 12 04 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/66972aa1-aec4-496f-b1a8-5167a0fe9120">
<img width="1168" alt="Screenshot 2024-05-11 at 12 23 16 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/29929fe2-cfcb-4ff7-a03f-a508046d48f2">

*Why so?*

ApplicationContext creates a Spring container for us. The container will have spring beans. The classes are specified in the xml file. Spring container checks the file and 
creates beans accordingly.

<img width="502" alt="Screenshot 2024-05-11 at 12 18 35 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/d8592d51-1744-4466-ab6f-b57b320ae585">

By default Spring follows Singleton pattern i.e. it gives only one instance of a class. Even if we ask multiple times, it will give the same instance.
All the Spring beans are called Singleton beans because objects are created only once. All the references refer to the same object.
For example, even though obj2 didn't set age, it still prints 15(the age set by obj1. 
<img width="1372" alt="Screenshot 2024-05-11 at 9 07 46 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/e14f6fc8-8b98-4a10-94be-30ff902ecf26">

*What if we don't want to follow singleton pattern?*
We can use a different scope.
Prototype means whenever we ask for a bean, Spring container creates an object at that time. So even if we ask 10 time, it will give 10 different instances of the class.
<img width="972" alt="Screenshot 2024-05-11 at 9 16 15 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/bfab0a72-c3ee-4b66-b76f-b1ef7d9b8531">
in case of Singleton, even if we dont ask for an object, Spring container creates and keeps the object ready for future use. However, when the scope is changed to Protoype, objects are created only when we ask for it.

# **Setter Injection**
<img width="915" alt="Screenshot 2024-05-11 at 9 31 34 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/8462b743-5c83-4e5a-9d35-86005016b9be">
<img width="1359" alt="Screenshot 2024-05-11 at 9 31 46 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/11bc46d7-61d1-43e9-b87e-651f95d2e1ae">
**Ref Attribute**
Create a bean of the new class. Reference can be added by using property "ref"
<img width="911" alt="Screenshot 2024-05-11 at 5 57 05 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/490abac8-6287-41d9-8452-60fffe5256d7">
<img width="845" alt="Screenshot 2024-05-11 at 5 57 15 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/3f50b3a4-3476-4245-974b-69871ed072fb">

# **Constructor Injection**
By default, the Spring container calls the default constructor. To call parameterized constuctor, tag "constructor-arg" can be used.
<img width="895" alt="Screenshot 2024-05-11 at 6 05 26 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/7ed9e6c8-116e-49c2-8177-18c01614fb24">
<img width="891" alt="Screenshot 2024-05-11 at 6 05 43 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/073b8869-6b70-44d0-bd51-e4160b118d56">

*Note: Property values can be injected by three ways*
  * value as a property
  * value as a tag
  * using p schema

  <img width="591" alt="Screenshot 2024-05-12 at 9 16 41 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/8439e2e7-2c18-40ff-9f4f-f1fd2a169865">
  <img width="962" alt="Screenshot 2024-05-12 at 9 20 16 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/6a1eed3f-5a55-4328-932a-2622817fd01b">
  <img width="979" alt="Screenshot 2024-05-12 at 9 20 37 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/de2d34c3-c2d8-43bb-b983-86c6de417087">
  <img width="1105" alt="Screenshot 2024-05-12 at 9 21 10 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/815175e6-5d1f-4afa-9764-765d0d6fbe72">
  <img width="1075" alt="Screenshot 2024-05-12 at 9 21 34 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/0c130211-a381-4d26-8d30-54c6adf53cb8">

# **Autowire**
If there are multiple implementations of an Interface, instead of manually adding reference of bean in property, autowire can be used. So
in case of autowire, we don't have to mention the property. It searches for a particular bean automatically based on name/type.
Hence, Autowire can be done byName or byType.
- byName: In this case, autowiring is done based on the name of the object. It will try to match name of the variable with that of the bean.
  For example, the bean id is "computer" and the variable name is "computer" as well.
  <img width="852" alt="Screenshot 2024-05-11 at 8 00 16 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/5437ba13-ad8e-4d57-acca-ea8c1b14fa43">
  <img width="847" alt="Screenshot 2024-05-11 at 8 00 45 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/fc94fe8d-6ece-4ec0-8c1d-9eead7bff5b2">
- byType: It doesn't just depend on the name of the object but type of the object as well. So, we can just declare a single bean of the same
  type of the targetted class as well and it should work.
  For exaple, Desktop implements computer and type of the variable in Alien class is Computer. So if a bean exists in the xml file, the
  spring container will autowire Desktop with Computer.
  <img width="892" alt="Screenshot 2024-05-12 at 8 27 41 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/d817ba0d-6d5b-4a35-8446-35953de5a260">
  <img width="957" alt="Screenshot 2024-05-12 at 8 27 52 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/9499edf1-4130-44c1-badf-d329b3d7fac7">
  <img width="955" alt="Screenshot 2024-05-12 at 8 28 02 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b92628ec-c42d-49df-bd7f-fcaae3240e03">

  However, spring container might get confused if there and multiple beans and autowiring is done by type.
  <img width="1340" alt="Screenshot 2024-05-12 at 8 36 19 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/99932428-3d45-46a3-9bfb-1d1ef843cbd7">
  The issue can be solved by 2 ways:
  * We can just remove autowiring and make use of property where we can mention the reference.
    <img width="949" alt="Screenshot 2024-05-12 at 8 41 54 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/7940b08b-0654-4d03-b6cf-7e0b1319d66e">
    <img width="679" alt="Screenshot 2024-05-12 at 8 42 16 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/860dd3ac-bf88-47ef-9dde-768031d4094e">
  * If we use autowiring, we can add a property in one of the beans(which we want to use) as primary.
    <img width="963" alt="Screenshot 2024-05-12 at 8 42 40 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/91fedf15-e91e-4387-8e97-4cef12f85264">
    <img width="1219" alt="Screenshot 2024-05-12 at 8 43 12 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/7828d50d-191b-4674-81bf-2f8248b04cea">

































  


