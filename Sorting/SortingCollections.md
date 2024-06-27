## Collections Class in java

Collections class in Java is one of the utility classes in Java Collections Framework. The java.util package contains the Collections class 
in Java. Java Collections class is used with the static methods that operate on the collections or return the collection. All the methods of 
this class throw the NullPointerException if the collection or object passed to the methods is null.  

The syntax of the Collections class declaration is mentioned below:

```
public class Collections extends Object
```

#### Note: Object is the parent class of all the classes.

<img width="1006" alt="Screenshot 2024-06-27 at 6 48 31 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/cb3f114e-4268-4ec9-a2d0-aef8f5c0a4a8">

Consider an ArrayList.

<img width="635" alt="Screenshot 2024-06-27 at 2 39 37 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7f4a5f47-4a40-4d40-846e-82988825fa16">

To sort, we can use Collections.sort(list)

<img width="664" alt="Screenshot 2024-06-27 at 2 39 44 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/91019878-d98e-45d9-8c74-7ca3b1387f79">

## Comparable

### How to sort custom object?

Let's create a Class named "Song".

<img width="710" alt="Screenshot 2024-06-27 at 2 59 07 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/bd956d14-e338-4ec3-b7be-51016067e128">

When we try to sort using Collections.sort method, we would notice that it gives a compile time error.

<img width="936" alt="Screenshot 2024-06-27 at 5 20 29 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/5b57831a-c192-43de-9cd6-94fc9e10a7e3">
<img width="649" alt="Screenshot 2024-06-27 at 5 21 28 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/89647507-27a0-4794-88de-2c91987152a5">
<img width="841" alt="Screenshot 2024-06-27 at 5 21 45 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/15c8d47e-48b8-409c-bf40-a2328390c02d">

#### Why so?

If we check javadoc, we would notice that "sort" method compare and sorts a List of any Type provided it should extend Comparable Interface.

<img width="1124" alt="Screenshot 2024-06-27 at 5 23 54 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9c9ffdec-e42d-4e6a-8fea-4efe91640913">

Comparable is an Interface which has one abstract method i.e. "compareTo. 

<img width="728" alt="Screenshot 2024-06-27 at 5 34 49 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/641e0cf4-64f2-4e90-89a7-e6cced56ebd4">
<img width="981" alt="Screenshot 2024-06-27 at 5 34 57 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a2e95017-7964-4e57-9346-0db9687b724a">

-------------------
### Let's take an example:

<img width="761" alt="Screenshot 2024-06-27 at 5 30 19 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a45c63c1-f654-4331-99d6-c4efd95e5a7c">
<img width="823" alt="Screenshot 2024-06-27 at 5 30 56 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7ea7c29e-82a3-440c-aba4-613ece2f4962">
-------------------

We can check and see that all Objects that can be used by "sort" extends Comparable

<img width="1019" alt="Screenshot 2024-06-27 at 5 32 44 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/901fed1a-a603-40d9-884b-8479ae6a880a">
<img width="1022" alt="Screenshot 2024-06-27 at 5 33 32 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8c2d894e-a657-4097-8bba-cd417919a599">

Let's come back to our Song example.

Let's say we want to sort the songs list based on year. To do this, we need to first extend Comparable Interface.

<img width="913" alt="Screenshot 2024-06-27 at 5 33 57 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a4d1bb8e-fda7-4aea-b352-65040d8cf3ca">

As with any other Interface, we need to implement the abstract methods

<img width="1148" alt="Screenshot 2024-06-27 at 5 34 20 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/99943fc5-06ec-4e3a-84de-0cf5241e5ae9">

Let's try to implement compareTo method

------------------
### How does compareTo work though?

<img width="686" alt="Screenshot 2024-06-27 at 5 41 06 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a235f00f-70f1-448b-8162-b04f4130f494">

- If first object is smaller than second -> it returns a negative integer

  <img width="705" alt="Screenshot 2024-06-27 at 5 41 23 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ba49383a-146b-4a2e-b0f9-0cc46152df93">
  <img width="1017" alt="Screenshot 2024-06-27 at 5 41 57 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/e1574f10-5f28-4310-af6d-f898f0831be3">
  <img width="750" alt="Screenshot 2024-06-27 at 5 45 07 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c7cb8252-419f-409b-99c9-b8c9ffa811d1">
  <img width="732" alt="Screenshot 2024-06-27 at 5 45 17 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/20facc32-11f0-4d43-90d7-3c3507d7dd3e">

- If first object is greater than second -> it returns a positive integer

  <img width="707" alt="Screenshot 2024-06-27 at 5 42 16 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/bf0a0dfc-1ebb-4424-8297-24811a46d33f">
  <img width="1091" alt="Screenshot 2024-06-27 at 5 42 36 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d522481b-41b5-45e0-8c1f-623dd71d367c">
  <img width="729" alt="Screenshot 2024-06-27 at 5 42 42 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/658a2333-1355-4c71-8fc4-8db25f493339">

- If first object is equal to second -> it returns 0

  <img width="668" alt="Screenshot 2024-06-27 at 5 43 28 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/6dca6358-2fc3-4662-9636-c68144a76bf0">


<img width="1039" alt="Screenshot 2024-06-27 at 5 40 26 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/edb103a4-efb7-47cd-9f30-6c458f231f0a">
<img width="1031" alt="Screenshot 2024-06-27 at 5 40 48 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/cf948560-fc3f-49f5-88b1-c31756f82662">

-------------------

<img width="1039" alt="Screenshot 2024-06-27 at 5 35 10 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/46258b43-8931-4607-9274-f7e4b667230a">
<img width="1065" alt="Screenshot 2024-06-27 at 5 37 55 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9b6dfb77-226a-4d8c-8051-4316e3aef5f9">
<img width="1156" alt="Screenshot 2024-06-27 at 5 37 59 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ee8696dc-6f4d-41ef-8cb7-7eb5442127ff">
<img width="1109" alt="Screenshot 2024-06-27 at 5 38 06 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/59030206-c9b3-4d78-8c07-cb0f264294f1">
<img width="832" alt="Screenshot 2024-06-27 at 5 47 36 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/f8bbdabe-aeb2-4efe-80c2-1cc1723418b4">
<img width="696" alt="Screenshot 2024-06-27 at 5 48 34 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b8c56e7a-da23-469d-a16a-40295f6687df">
<img width="781" alt="Screenshot 2024-06-27 at 5 48 53 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/07a938d5-cbef-4c22-b01e-14ec1070291d">

<img width="1077" alt="Screenshot 2024-06-27 at 5 49 15 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/fa938c97-4d09-40fa-b512-86ce6546d29e">
<img width="812" alt="Screenshot 2024-06-27 at 5 50 22 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d4506a52-d93b-4964-a28c-d360dd3e4a1e">
<img width="873" alt="Screenshot 2024-06-27 at 5 50 39 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/16918212-88ef-43ce-a695-c22a000073a7">
<img width="615" alt="Screenshot 2024-06-27 at 5 51 17 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/72be574c-9f94-419b-a3d4-24638e718291">
<img width="1050" alt="Screenshot 2024-06-27 at 5 51 41 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/03df1532-01b8-409a-b3ea-2ff04560d29a">
<img width="759" alt="Screenshot 2024-06-27 at 5 52 09 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/84cb37a7-b675-4e55-b76f-d9163daa5672">

If we want to sort in descending order,

<img width="1000" alt="Screenshot 2024-06-27 at 5 52 42 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c409da9d-73f0-484d-9bdc-fa53b0daea5a">
<img width="780" alt="Screenshot 2024-06-27 at 5 52 51 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d801b60f-fc34-42ad-b5d6-0c07dd0aa551">

## Comparator

<img width="1125" alt="Screenshot 2024-06-27 at 5 24 06 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ecf932a5-05bf-4d48-9ede-b271bdd2187a">

#### There are 2 methods in Comparator interface which is abstract - compare & equals. But it only asks us to implement compare. Why so?

Every Class by default extends Object class and the "equals" method is already implemented there. So it doesn't throw any error 
if we don't imlement the equals method.

<img width="1089" alt="Screenshot 2024-06-27 at 6 10 30 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/4fbe64ec-ccd7-48a9-b429-301c24058c8e">
<img width="1093" alt="Screenshot 2024-06-27 at 6 11 34 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/6878f50b-d40c-4882-b360-89c5753caa06">
<img width="1057" alt="Screenshot 2024-06-27 at 6 12 17 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2001460f-3235-478c-b536-78bb78e9edfb">


<img width="746" alt="Screenshot 2024-06-27 at 6 08 26 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/bc52542e-7d96-4331-903a-bae0caa89645">
<img width="1073" alt="Screenshot 2024-06-27 at 6 08 45 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/810c3564-0713-419d-baf8-be8b785899c8">
<img width="1127" alt="Screenshot 2024-06-27 at 6 09 32 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/3a2e7001-d75e-4b00-b5ba-1995cb290e3a">
<img width="1032" alt="Screenshot 2024-06-27 at 6 10 05 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/3e92aa94-8aad-4189-b089-c4802330d8e9">
<img width="1144" alt="Screenshot 2024-06-27 at 6 14 19 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8b00aecb-fe9e-4fea-aa18-f8c5e958cfe4">
<img width="763" alt="Screenshot 2024-06-27 at 6 19 28 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/24cfa7fa-5864-488f-aa04-1590aade6c36">
<img width="1022" alt="Screenshot 2024-06-27 at 6 20 16 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/03902b13-4f3d-4b06-a63e-7c77e13bcb81">
<img width="1118" alt="Screenshot 2024-06-27 at 6 20 54 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/92741a56-e0f5-4792-9143-c58eee5f7cec">

### Question

<img width="1077" alt="Screenshot 2024-06-27 at 6 21 51 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2078b46b-ba96-422b-b754-0c8ab19a6fc6">
<img width="913" alt="Screenshot 2024-06-27 at 6 23 18 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/1bce88a1-9bf2-4a46-a18d-e154c7ff0519">
<img width="869" alt="Screenshot 2024-06-27 at 6 23 49 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/1293f0ea-0af4-4e4d-b31c-3bfdd2109127">
<img width="1032" alt="Screenshot 2024-06-27 at 6 24 20 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/6061ad3f-a7e8-4019-9c1d-56191b92229c">

