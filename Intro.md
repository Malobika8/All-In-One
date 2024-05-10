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
<img width="650" alt="Screenshot 2024-05-11 at 12 12 11 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b17afd36-b006-4e76-9016-61d8ddafd7f8">

*Why so?*

ApplicationContext creates a Spring container for us. The container will have spring beans. The classes are specified in the xml file. Spring container checks the file and 
creates beans accordingly.

<img width="502" alt="Screenshot 2024-05-11 at 12 18 35 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/d8592d51-1744-4466-ab6f-b57b320ae585">






  


