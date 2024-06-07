# Different ways to create an object

#### Q1. How to create an object without using new keyword?
#### Q2. What are the different ways to create an object in java?
#### Q3. In which way of object creation the constructor doesn't get called?

1. Using the "new" keyword:

   <img width="963" alt="Screenshot 2024-06-07 at 8 48 30 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/23c4bcd4-9881-42d2-9aeb-060820bda966">

2. Using NewInstance() of Class: The method newInstance() belongs to a class "Class"(java.lang.Class).

   Steps:
     - Load the class
       - Class.forName(\<Fully-Qualified-ClassName\>)
       - <Classname>.Class.newInstance()
     - Class newInstance() method
     - Perform operations
  
     <img width="933" alt="Screenshot 2024-06-07 at 8 58 06 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/dafb678c-fd3b-4634-b900-c145a1575ccb">
     <img width="923" alt="Screenshot 2024-06-07 at 9 01 04 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/809dff9e-54d9-4f90-9a23-17e95ff8f934">

3. Using Constructor.newInstance(): There is a class called "Constructor" in "java.lang.reflect" package.

   <img width="1104" alt="Screenshot 2024-06-07 at 9 04 16 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/2fae2d33-b71c-4784-82eb-5eebadd661df">

   Class.newInstance() - 
   
   <img width="453" alt="Screenshot 2024-06-07 at 9 04 38 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/9e530cee-84a8-40e3-8b55-c51c9b706b6c">
   <img width="447" alt="Screenshot 2024-06-07 at 9 05 26 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/792a003b-4ab4-4170-b80e-c93dbe89b7bc">
   <img width="430" alt="Screenshot 2024-06-07 at 9 05 51 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/1f4fc74c-7f9f-42c2-a6d1-874d226ec139">

   Constructor.newInstance() - 
   
   <img width="499" alt="Screenshot 2024-06-07 at 9 04 45 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/f7daa4c5-8606-494a-872b-e16961c039a3">
   <img width="488" alt="Screenshot 2024-06-07 at 9 05 33 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/fef58b81-e336-4221-be16-60649a10730b">
   <img width="473" alt="Screenshot 2024-06-07 at 9 06 15 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/2aa0670a-aef5-46fd-98f0-f8f740b25e63">

   *Note:* Class.newInstance always calls Constructor.newInstance internally. Frameworks like Spring, Struts, Hibernate creates object using Constructor.newInstance. This way of object
   creation is called Reflective way of object creation.

   <img width="1055" alt="Screenshot 2024-06-07 at 9 09 28 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/dd1a9114-e183-4cf0-b5a3-2a55f53ca0e5">
   <img width="932" alt="Screenshot 2024-06-07 at 9 13 55 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/0dd94f08-4a77-41ee-b8a5-d7a3e07dbb98">

4. Using clone() method of "Object" class: Copying an object. To clone, the original class should implement Cloneable and override clone() method.

  *Note:* The constructor doesn't get called.

  <img width="925" alt="Screenshot 2024-06-07 at 9 21 17 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/57efc1ff-6a2a-4007-ac76-844edb4b2c69">
  <img width="934" alt="Screenshot 2024-06-07 at 9 22 32 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/6f8acde0-d686-45d7-9d84-7dcd15478b17">

5. Using Deseralization:

   *Note:* The class to be Deserialized should implement Serializable.

   <img width="990" alt="Screenshot 2024-06-07 at 9 25 22 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/f2188efe-2d2d-4173-8766-bb335d7bed54">
   <img width="866" alt="Screenshot 2024-06-07 at 9 31 44 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/afce1f68-ada5-4dae-8ac0-5d86f88c1eed">


