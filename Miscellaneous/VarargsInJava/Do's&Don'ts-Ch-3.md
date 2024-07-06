# Do's & Don'ts 

1. We can take both normal arguments & var-args together. 

   <img width="543" alt="Screenshot 2024-07-06 at 12 03 32 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/67e0722b-f7f9-437d-b866-d99ff3d3a30e">
   <img width="569" alt="Screenshot 2024-07-06 at 12 04 10 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/4e640da6-e01d-4da7-8a86-538372697245">

   ### Note:
   var-args should be last in the method parameter list. Otherwise, it will throw a compile-time error.

   <img width="502" alt="Screenshot 2024-07-06 at 12 07 48 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/76562a99-e8c3-43c7-bc97-2cc7d00fee83">
   <img width="1020" alt="Screenshot 2024-07-06 at 12 08 12 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/009b0a60-8578-4050-867a-e19dc42c8f72">
  
   We can have different parameter types as well.

   <img width="695" alt="Screenshot 2024-07-06 at 12 06 12 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/1ed42b93-c299-4544-9dd4-f447bd85ea4d">

2. We cannot take more than one var-args in a method as it will then violate the rule of var-args being the last parameter in the list.

   <img width="704" alt="Screenshot 2024-07-06 at 12 11 37 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a7fc7e5e-b2d0-41a1-bd55-780cdbc56a0c">

3. var-args methods are dangerous to overload as it is always given last priority by JVM.

   The following piece of code is not allowed as both of them are essentially the same.

   <img width="821" alt="Screenshot 2024-07-06 at 12 16 39 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b338a989-25d6-482d-9038-24c19bcedb24">

   It will throw a Compile-Time error.

   <img width="1083" alt="Screenshot 2024-07-06 at 12 17 21 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/344823d3-82ab-4f7f-96bb-0d49d41a2801">

   ### Why varargs overloading is not a good idea?

   Consider the following program.

   <img width="755" alt="Screenshot 2024-07-06 at 12 22 28 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/994a2c65-eaee-4400-8cba-ff621f6d0ff4">

   It looks ambiguous but it compiles fine.

   ### If we run it, which one would be called though? Both methods can handle it.

   <img width="745" alt="Screenshot 2024-07-06 at 12 21 46 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/f9d23090-655f-4c6e-aecf-27f0cfd99d8a">

   When we try to call the method, it throws a compilation error as both methods can handle the request.

   <img width="1012" alt="Screenshot 2024-07-06 at 12 24 56 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/6ea9f186-abcb-4e25-9a8e-dcd1d27b93a1">
   
### Question

#### Find out the reason behind the following behavior.

The following program compiles fine without any warning.

<img width="772" alt="Screenshot 2024-07-06 at 12 29 40 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/05daa70c-fd82-4cf7-bc14-5d558ddd830b">

It throws a warning when we try to pass only a single *null* argument

<img width="522" alt="Screenshot 2024-07-06 at 12 30 50 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/18fc70cb-0288-4bd2-bbc9-80db2923ca14">
<img width="529" alt="Screenshot 2024-07-06 at 12 31 10 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/cbd51fed-4537-422a-9a3b-fce379a2ff40">

It works fine when casting it to *Object*.

<img width="686" alt="Screenshot 2024-07-06 at 12 32 25 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d22e85db-324b-42ef-bbca-51b927a4551d">

Output:

<img width="261" alt="Screenshot 2024-07-06 at 12 32 49 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/afd732a0-cf00-49cf-8320-e9f0e315c173">

