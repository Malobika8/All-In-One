# **Good to know info**
* Developer - Rod Johnson
* Org- spring org/pivotal
* Initial name - Interface 21 (later changed to Spring)

Spring has become an alternative technology in Java world for the EJB model. Spring is lightweight as compared to ejb's.
Why AWT's are heavy weight and not Swings? Because the AWT's uses OS libraries but not swings. Swings just use jdk libraries.
Similarly, for ejb's, application server is needed. In case of Spring, only spring jars and jdk is required.
We have different frameworks available for different needs like struts for web development, ejb for enterprise application & jpa for database. Spring handles all of it.

**Why Spring? -** Because developers should focus on business logic leaving aside creating and managing objects. Config file can be used to 
store class related info. 

<img width="1115" alt="Screenshot 2024-05-15 at 12 22 34 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/e15b5000-f600-49d5-b5db-b29ff4fb63ef">

Spring has its own container called IOC container. It reads the config file and create/manage objects for all the classes specified. 
**The objects created by spring are called beans** (Objects in the IOC container).

<img width="1132" alt="Screenshot 2024-05-15 at 12 30 54 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/e41fa5ca-749a-412b-b391-9fbaad74cde9">

How to get the object? - Using getBeans method.

<img width="1134" alt="Screenshot 2024-05-15 at 12 40 53 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/0f8c51e3-b2be-4944-bf47-6c082245b9da">

How to use the IOC Container? - 

<img width="1134" alt="Screenshot 2024-05-15 at 12 43 10 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/ab928dc3-1398-4740-bf27-bfc829bb00e8">

ApplicationContext has some additional features as compared to BeanFactory. It is more advanced. Beanfactory is still there to support backward compatibility. These are both Interfaces.
ClasspathXMLApplicationContext is the implementation of ApplicationContext.

<img width="1131" alt="Screenshot 2024-05-15 at 12 56 53 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/c19d98ca-9f2d-4487-b9bc-a6e1219be6fb">

Example: Config when there's multiple implementations of an interface. The fully qualified classname should be of the implementation class.

<img width="634" alt="Screenshot 2024-05-15 at 1 11 28 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/8dd5978b-4ef7-4574-bb6d-bd0fa95ee553">
<img width="660" alt="Screenshot 2024-05-15 at 1 11 34 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/ea747794-c2ec-4a96-9923-be9edfd0c750">
<img width="311" alt="Screenshot 2024-05-15 at 1 11 39 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/2a2d32f7-664b-4cd7-a071-b785a4a4871e">
<img width="961" alt="Screenshot 2024-05-15 at 1 11 47 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/919ffa9f-513b-4ec4-ae19-6388265ef111">
<img width="961" alt="Screenshot 2024-05-15 at 1 12 00 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/0bef9ce5-2846-45fa-8d57-a5c1d6501e05">
<img width="753" alt="Screenshot 2024-05-15 at 1 12 14 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/2ec41c84-b6aa-466e-81c8-f307c19f11d1">

**Inversion of Control**: Framework creates and manages the object for us rather than us doing the same manually. The framework takes care of dependency control as well.

<img width="1128" alt="Screenshot 2024-05-15 at 1 17 30 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b655c53f-86ae-4f7f-a7c7-1c678c669fd2">


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






















  


