## Executable SpringBoot Jar

##### Let's say we are done with development and our Application is ready. How to deliver the Application to a Client?

We can build a Jar/War and run it on a server(aws or any hosting server) and go live.

#### But how to build a Jar and deploy?

- Maven build: *mvn clean install*

  Jar file gets generated in **Target** folder with some other files.

  ##### But we are building a web Application so how can we create a jar file out of it?

  This is a mordern Jar called **FAT JAR** (Jar which is embedded with server/web-server). This Jar contains which the files which we have
  written.

      Spring Boot is known for its “fat” JAR deployments, where a single executable artifact contains both the application code and all of
      its dependencies. Boot is also widely used to develop microservices.

      A Fat Jar is a type of JAR file that contains all the dependencies
      required to run an application. It is called a "fat" jar because it includes all the necessary libraries and dependencies in one file,
      rather than requiring them to be downloaded and installed separately. This makes it easier to deploy and run the application, as all the
      required dependencies are included in the same file. Fat Jars are commonly used in microservices architectures, where each service has its
      own dependencies and can be deployed as a standalone application.

- Run the Jar file

  Tradiitonally, we build Wars for Web Application (Jars for Desktop Applications) and run it on a Server. It is different for SpringBoot as
  it comes with a WebServer(Tomcat) embeded.

  <img width="423" alt="Screenshot 2024-06-21 at 7 30 47 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b33d14dc-2574-4758-8bfb-55ca6f105ed7">

  The Jar that is built not only has the files zipped but has all required dependencies added as well. So SpringBoot helps us create
  Standalone Applications.

  Let's see if we can run the Jar without any external Server.

  ##### i) Go to target folder where we have our Jar file

     <img width="525" alt="Screenshot 2024-06-21 at 7 35 39 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c0562907-8346-4f93-98da-10abccba6662">

  ##### ii) Open the same in terminal

     <img width="717" alt="Screenshot 2024-06-21 at 7 35 56 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c3a82eae-f69a-4197-a201-daba88191dfc">

  ##### iii) Run the Jar file

     <img width="805" alt="Screenshot 2024-06-21 at 7 37 55 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/f43d715a-b35e-4164-802f-1b532007e6cb">
     <img width="665" alt="Screenshot 2024-06-21 at 7 39 59 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ebe2a9e3-6abc-4b9f-abd3-f5b567009b35">

     ##### Why we are not able to run the Jar though?

     The Jar that we are creating should be a Fat Jar. There's a maven plugins that does just the same - **spring-boot-maven-plugin**

       The Spring Boot Maven Plugin provides Spring Boot support in Maven, allowing you to package executable jar or war archives and run an
       application “in-place”.  Spring Boot Maven Plugin is a tool used to facilitate the creation, building, testing, and deployment of
       Spring Boot applications. It simplifies the process of setting up a Spring Boot project and provides various features, like creating
       root packaging, generating starter dependencies, creating Maven configurations, and more. The plugin is built on top of Maven, a
       popular continuous integration framework, and can be used to automate the entire build, test, and deploy cycle for a Spring Boot
       application. To use it you must be using Maven 3.2 (or better).

     Add the below plugin:

      <build>
        <plugins>
          <!-- https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-maven-plugin -->
          <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
          </plugin>
        </plugins>
      </build>

     Build the Jar again and run it.

     <img width="328" alt="Screenshot 2024-06-21 at 7 52 50 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/4ce769ed-834d-44c8-841c-ed6268b0473a">
     <img width="862" alt="Screenshot 2024-06-21 at 7 53 08 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/51a223ef-d643-4c54-8284-551e321d2ef0">
     <img width="432" alt="Screenshot 2024-06-21 at 7 54 17 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/bedfde5f-0f41-4996-8975-289267dc8762">
     <img width="498" alt="Screenshot 2024-06-21 at 7 59 17 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/28a10ef5-2298-40da-818b-414bc972d537">

     #### But what if we want to run it on a different port?

     Earlier in IDE, we were adding the property in Run Configurations. This time we can directly mention the property while running the Jar.

     <img width="521" alt="Screenshot 2024-06-21 at 8 00 47 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b123dd1e-1ea3-4d9f-8152-a6482db0e1ba">
     <img width="424" alt="Screenshot 2024-06-21 at 8 00 54 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/66cd1f46-b6c9-4259-9515-257da3873ded">
     <img width="602" alt="Screenshot 2024-06-21 at 8 02 12 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/dba02f14-4529-4dfd-8938-d07d6acfdfe6">

# Difference between JAR & FAT JAR

### i) JAR: Less memory

   <img width="729" alt="Screenshot 2024-06-21 at 8 06 06 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/4f167787-ab55-4abf-ac8a-a8200e9c2de3">

   When we try to run it, we get "no main manifest attribute" error. This means it doesn't know what to run and where to start.

   <img width="581" alt="Screenshot 2024-06-21 at 8 07 02 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d67d8582-2ef2-4cfa-a10f-9a93e8b992cc">

   Let's try to unzip the jar and observe

   <img width="716" alt="Screenshot 2024-06-21 at 8 08 56 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9c6532f8-a669-43c1-975a-2a5de95af9d1">
   <img width="819" alt="Screenshot 2024-06-21 at 8 09 05 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/58f55a68-ba21-490c-a3f7-097a4e9cc8a0">

   We have a MANIFEST.MF file.

   <img width="842" alt="Screenshot 2024-06-21 at 8 09 31 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/0e2f0966-d919-414d-a6c5-7d5846e69f0e">

   We can see there's no start class, main method defined

   <img width="607" alt="Screenshot 2024-06-21 at 8 09 38 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/584ea43b-85ab-4066-8b91-b00c8eb6c4c5">
   <img width="1154" alt="Screenshot 2024-06-21 at 8 10 49 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2a131c0e-f0aa-4b0a-9fca-e3cae7a9928d">

   Basically it doesn't know where to start. What is the Class that would help in Bootstrapping the Application.

   Also, we can see all the classes are present but no dependencies.

   <img width="847" alt="Screenshot 2024-06-21 at 8 13 08 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/553b8ad5-5616-41ca-9e1e-6720870203cd">

   <img width="875" alt="Screenshot 2024-06-21 at 8 14 44 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/f4cfc927-1818-485b-8d97-5eab3e060f63">

### ii) FAT JAR: More memory

   <img width="850" alt="Screenshot 2024-06-21 at 8 16 48 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/034f202f-4e9d-45ab-b1cc-143a58c930fb">

   Let's try to unzip the jar and observe
   
   <img width="842" alt="Screenshot 2024-06-21 at 8 15 51 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/1f0a4844-0794-4f75-b7aa-d4d0f432160c">

   It looks very different

   <img width="875" alt="Screenshot 2024-06-21 at 8 17 40 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/e9091d61-beec-45b5-96b4-afa4f842d512">

   We can see all our dependencies present in lib folder

   <img width="826" alt="Screenshot 2024-06-21 at 8 17 51 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/106dd67d-d884-4381-97cd-d5022cb22654">

   All the classes available

   <img width="849" alt="Screenshot 2024-06-21 at 8 18 53 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/f5999257-faae-4925-a51a-ad71661132e1">

   Entry point to our Application is our "StarterApp" as it has a main method. From here, our program execution begins. The "run" method
   Bootstraps our Spring Application.

   <img width="521" alt="Screenshot 2024-06-21 at 8 19 14 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/14f41387-6d08-4abb-8b0e-a88920c1a4d8">

   #### When we run a Jar file how would Java know which Class would help us in starting the Application?

   We have MANIFEST.MF file in META-INF folder.

   <img width="712" alt="Screenshot 2024-06-21 at 8 22 47 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d3ce88a1-d13d-4224-aa08-27c53355d184">
   <img width="953" alt="Screenshot 2024-06-21 at 8 24 10 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/3c8b9eb6-a36a-41f3-864a-dba9a247e1a1">

   JarLauncher is basically a Launch/Batch File which helps in starting the Application.

   <img width="718" alt="Screenshot 2024-06-21 at 8 25 26 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/fb4d00c2-3851-4177-bc4b-dc883a8101de">
   <img width="761" alt="Screenshot 2024-06-21 at 8 26 02 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c01ace03-4b63-4e7e-a335-04badf75417a">
   <img width="894" alt="Screenshot 2024-06-21 at 8 28 52 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ceaad733-fb01-457a-9490-50d7a82fa28d">

## Questions

#### 1) Difference between Jar, War and Ear.
#### 2) Difference between Jar and fat Jar.
