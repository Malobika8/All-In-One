## Version management

We know that spring-boot-starter-parent does **Version Management** for us.

<img width="1124" alt="Screenshot 2024-06-22 at 7 29 34 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/22ef1d88-3a3f-43c0-9eb7-2830655e6f1b">

Lets say we want to change the Java version. We can go to spring-boot-start-parent pom and check the version that is currently being used.

<img width="857" alt="Screenshot 2024-06-22 at 7 40 36 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/0a6ab0d1-70fe-4c51-b620-1ef213f47706">

In order to change version, we can override the property in our pom.

<img width="688" alt="Screenshot 2024-06-22 at 7 41 14 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8a2c77a3-36c7-42f4-82a1-d810109454cb">
<img width="238" alt="Screenshot 2024-06-22 at 7 41 33 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/0957e1e4-7559-4b9b-821f-0273f7bd2152">

Let's try to understand how Version Management works.

Now, if we check spring-boot-starter-parent pom, we'll see there exist a parent pom, spring-boot-dependencies.
This is exactly where versions for all different dependencies are mentioned and from this, our project pulls in the dependency versions. It even
includes third-party libraries.

<img width="834" alt="Screenshot 2024-06-22 at 7 42 11 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a69c0fbb-31a3-4490-a458-a756b886fbe2">
<img width="854" alt="Screenshot 2024-06-22 at 7 42 38 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2ab872b4-31aa-44d5-a8b2-44d823849fd4">
<img width="828" alt="Screenshot 2024-06-22 at 7 43 47 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2e29f9cc-4ecf-4304-b1de-c88bdc106724">

In our project, we have a dependency called spring-boot-starter-web without version mentioned.

<img width="623" alt="Screenshot 2024-06-22 at 7 45 38 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a2bbb4ca-f97a-4db9-b501-a192bdf75b88">

The dependency version for the same is mentioned in spring-boot-dependencies which is parent of spring-boot-starter-parent(which is again our parent pom).
<img width="710" alt="Screenshot 2024-06-22 at 7 45 50 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/cfeea57f-515f-4e51-b50c-2ad62379d6cf">

We can check similarly for spring-webmvc.

<img width="469" alt="Screenshot 2024-06-22 at 7 46 08 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d67b92d7-8767-42aa-8994-52beba082087">
<img width="179" alt="Screenshot 2024-06-22 at 7 46 19 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/182e7730-4144-47ac-be9a-5e4ad39b363d">

## Jackson API for Rest Support

- Spring MVC:
  
  Let's go back to our **Spring MVC project**.

  Suppose we want to send back an object instead of simply returning a String when we hit the url. We want the content to be rendered in json format.

  <img width="684" alt="Screenshot 2024-06-22 at 8 04 37 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/1444db1f-c561-4f6e-9e98-0223a834c31f">

  When we hit the url, our object content should be displayed like this.

  <img width="742" alt="Screenshot 2024-06-22 at 8 04 46 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c8fb9006-5054-4305-baef-e4f0626c2c4a">

  However, when we try to hit the url, we come across an error (*No Acceptable Representation*).

  <img width="1147" alt="Screenshot 2024-06-22 at 8 05 54 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/169c3b4d-a969-4801-a8cd-172864f2a79b">
  <img width="799" alt="Screenshot 2024-06-22 at 8 06 02 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c81b30dd-80f0-4db1-822e-91865f8e03c2">

  So, how should we convert our Java object to a Json object?

  <img width="824" alt="Screenshot 2024-06-22 at 8 06 29 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/e256bc73-dd84-479a-920b-37f7c45f8855">

  We would require to add two dependencies - *jackson-core* & *jackson-databind*

  <img width="799" alt="Screenshot 2024-06-22 at 8 07 23 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/77c1ef89-0478-445f-a75d-91401450fb91">
  <img width="795" alt="Screenshot 2024-06-22 at 8 07 42 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/23d14a87-ef3e-4698-8363-1f9839218428">

  Additionally, we would require a Converter to do the conversion, from Java to Json object, for us. To do that, we can simply use an annotation, *@EnableWebMvc*.

  <img width="848" alt="Screenshot 2024-06-22 at 8 09 07 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/82df4138-d5c4-4bed-8dea-26bf4d8f7a0d">

  Let's update our Maven project.

  <img width="506" alt="Screenshot 2024-06-22 at 8 08 01 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/06cdfd69-1458-4cbb-88c3-2219e240042c">

  This time, the Java object should be successfully rendered in Json format when we hit the url.

  <img width="642" alt="Screenshot 2024-06-22 at 8 08 37 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/03702e99-50fb-487c-84f9-1601b1fb4ea8">
  <img width="656" alt="Screenshot 2024-06-22 at 8 09 24 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/3d61bb41-9b74-4214-9dcd-7941fcf3ce09">

- SpringBoot:

  We don't have to do any kind of setup in SprinBoot in order to expose any Json object to the outer world. It is automatically handled.

  There is a "spring-boot-starter-json" dependency that is pulled in by "spring-boot-starter-web" that handles all. Spring knows that in certain
  situation, we might require conversion from Java to Json object which would need Jackson jars and Converter.

  <img width="381" alt="Screenshot 2024-06-22 at 7 59 46 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/3d85d749-eeab-4a04-907f-b17c11148427">
  <img width="431" alt="Screenshot 2024-06-22 at 10 07 00 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/5b1b8b8e-b4a6-43b8-a4eb-50da16398db5">
  <img width="1109" alt="Screenshot 2024-06-22 at 10 00 04 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/31c8c722-66df-468d-9312-7dfcb1709a6c">
  <img width="739" alt="Screenshot 2024-06-22 at 10 00 44 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b3eac8b5-a6c6-4cb2-90b2-27a83fb0e0e2">

