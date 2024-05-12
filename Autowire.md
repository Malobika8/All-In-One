# **Autowire**

<img width="1066" alt="Screenshot 2024-05-12 at 11 17 49 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/5e6ae962-8385-48a8-9468-c86261d4350b">
<img width="905" alt="Screenshot 2024-05-12 at 11 18 49 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b428f3cb-bd2f-4a0e-940f-442d708eeb0d">

If there are multiple implementations of an Interface, instead of manually adding reference of bean in property, autowire can be used. So
in case of autowire, we don't have to mention the property. It searches for a particular bean automatically based on name/type.

# **Through XML config**
Autowire can be done byName or byType.

<img width="912" alt="Screenshot 2024-05-12 at 11 21 45 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/de01e6b4-230f-47fa-9c96-4f28c7ef6d01">

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

# **Through annotations**

If @Autowired annotation will be added on :
1) property , only default constructor will be called.
2) setter method , both default constructor and setter method will be called.
3) parameterised constructor , only parameterised constructor will be called.
4) default constructor , only default constructor will be called, but property will remain as *null*.
- Can be used over a property. Only default constructor will be called.

  <img width="778" alt="Screenshot 2024-05-12 at 11 41 35 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/52354381-7cad-406f-a66d-271a8f918f2d">
- Can be used over a setter method. Both default constructor and setter method will be called.

  <img width="771" alt="Screenshot 2024-05-12 at 11 42 29 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/7a390aa3-d233-4bd5-ac10-71f996db5ae9">
  <img width="848" alt="Screenshot 2024-05-12 at 11 44 35 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/cd88fc93-18b9-4262-a8c7-cb9840623895">
- Can be used over a constructor.
  * Parameterised constructor - only parameterised constructor will be called.
  * Default constructor - only default constructor will be called, but property will remain as *null*.

  <img width="754" alt="Screenshot 2024-05-12 at 11 42 47 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/22ceb45b-c988-4844-807b-5bb30d27bc27">
  <img width="663" alt="Screenshot 2024-05-12 at 11 44 10 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/f9290c96-e851-4b4f-9ced-e7358a6881a7">

# **Advantages/Disadvantages**
<img width="962" alt="Screenshot 2024-05-12 at 11 22 48 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/d70e1140-59c1-42a1-a35c-0805c707083c">
