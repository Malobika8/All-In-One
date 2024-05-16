Dependency Injection

# **Dependency Injection**
Injecting a value to the dependency.
The Dependency Injection is a design pattern that removes the dependency of the programs. In such case we provide the information from the external source such as XML file. It makes our code loosely coupled and easier for testing. In such case we write the code as:

    class Employee{  
    Address address;  
  
    Employee(Address address){  
    this.address=address;  
    }  
    public void setAddress(Address address){  
    this.address=address;  
    }  
    }  
    
In such case, instance of Address class is provided by external souce such as XML file either by constructor or setter method.

# **Types of Spring Dependency Injection:**
* **Setter Injection**
* 
  With "property" tag in place, spring looks for setter method for the property specified.
  <img width="1149" alt="Screenshot 2024-05-15 at 6 06 00 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/40023619-f8dc-455e-8481-135276f2d4cf">

  *What is happenning internally?*

  <img width="1147" alt="Screenshot 2024-05-15 at 6 07 37 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/bc921b6c-3b4e-4a05-a2ae-53c9b85730c1">

  <img width="915" alt="Screenshot 2024-05-11 at 9 31 34 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/8462b743-5c83-4e5a-9d35-86005016b9be">
  <img width="1359" alt="Screenshot 2024-05-11 at 9 31 46 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/11bc46d7-61d1-43e9-b87e-651f95d2e1ae">
  **Ref Attribute**
  Create a bean of the new class. Reference can be added by using property "ref"
  <img width="911" alt="Screenshot 2024-05-11 at 5 57 05 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/490abac8-6287-41d9-8452-60fffe5256d7">
  <img width="845" alt="Screenshot 2024-05-11 at 5 57 15 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/3f50b3a4-3476-4245-974b-69871ed072fb">

* **Constructor Injection**

  In case of constructor injection, irrespective of the type, the value can be passed as String as Spring detects the type associated by itself.

  <img width="1095" alt="Screenshot 2024-05-16 at 11 05 44 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/8909026b-104e-4591-87cc-f8ad7c1ce057">

  The type can be explicitely defined as well.

  <img width="967" alt="Screenshot 2024-05-16 at 11 44 03 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/c6f16155-819e-4834-b130-d387d9c85acb">
  
  By default, the Spring container calls the default constructor. To call parameterized constuctor, tag "constructor-arg" can be used.
  
  <img width="895" alt="Screenshot 2024-05-11 at 6 05 26 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/7ed9e6c8-116e-49c2-8177-18c01614fb24">
  <img width="891" alt="Screenshot 2024-05-11 at 6 05 43 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/073b8869-6b70-44d0-bd51-e4160b118d56">

  Another way to inject reference

  <img width="887" alt="Screenshot 2024-05-16 at 1 02 21 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/86dc4434-b22a-47c9-8df9-72e0e8829caa">
  <img width="547" alt="Screenshot 2024-05-16 at 1 09 33 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/1cd67b83-0f9a-4698-89c7-95f46957933d">

  This is not a good approach though as bean gets configured multiple times in case of injecting a common reference to multiple classes. Since, the object gets created multiple
  times, the application becomes heavy weight.
  
  <img width="756" alt="Screenshot 2024-05-16 at 1 25 12 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/fa619c60-dfb8-4467-aeb4-dca614594368">
  <img width="1114" alt="Screenshot 2024-05-16 at 1 30 07 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/5f491f2e-eb49-4b4e-a014-be57eacd35e6">
  <img width="485" alt="Screenshot 2024-05-16 at 1 31 37 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/14fc4d35-7ece-4bce-8b5e-405fb5d72c66">

  Better way is to create a bean once and reference it using "ref".

  <img width="505" alt="Screenshot 2024-05-16 at 1 38 02 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b2423838-3076-4aee-b0ef-ab2d9aa483d2">
  <img width="494" alt="Screenshot 2024-05-16 at 1 38 15 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/c22fed17-2af6-4cc6-b040-8fe3ae2f197a">
  <img width="1150" alt="Screenshot 2024-05-16 at 1 39 17 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b23d14c9-8206-4f86-b927-328f3800cbb0">

  # *Note: Property values can be injected by three ways*
    * value as a property
    * value as a tag
    * using p schema

  <img width="591" alt="Screenshot 2024-05-12 at 9 16 41 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/8439e2e7-2c18-40ff-9f4f-f1fd2a169865">
  <img width="962" alt="Screenshot 2024-05-12 at 9 20 16 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/6a1eed3f-5a55-4328-932a-2622817fd01b">
  <img width="979" alt="Screenshot 2024-05-12 at 9 20 37 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/de2d34c3-c2d8-43bb-b983-86c6de417087">
  <img width="1105" alt="Screenshot 2024-05-12 at 9 21 10 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/815175e6-5d1f-4afa-9764-765d0d6fbe72">
  <img width="1075" alt="Screenshot 2024-05-12 at 9 21 34 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/0c130211-a381-4d26-8d30-54c6adf53cb8">

# **Interface**
In case of interface, we can provide the implementation required.
Example,

<img width="972" alt="Screenshot 2024-05-16 at 5 41 35 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/e7e27b8c-943e-4652-a2ef-b3e3d21a0ec6">
<img width="1158" alt="Screenshot 2024-05-16 at 5 41 58 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/ca9417e7-acee-4987-a993-ae1a569b440f">















