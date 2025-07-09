# Let's try to build Discovery Service Component.
## Steps to create a Discovery Server
1. Create a new project for DiscoveryService. Add annotation *@EnableEurekaServer*.

   <img width="966" alt="Screenshot 2024-07-13 at 9 26 51 AM" src="https://github.com/user-attachments/assets/e9563bc4-df21-4bc8-8f5a-d8e3b5a4155a">

2. Dependency required:

   ```
    <dependency>
      <groupId>org.springframework.cloud</groupId>
      <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
    </dependency>
   ```

   pom.xml

   ```
    <parent>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-parent</artifactId>
      <version>3.3.1</version>
    </parent>
    <groupId>org.example</groupId>
      <artifactId>DiscoveryService</artifactId>
      <packaging>war</packaging>
      <version>1.0-SNAPSHOT</version>

      <name>DiscoveryService Maven Webapp</name>
      <url>http://maven.apache.org</url>
      <dependencies>
        <!-- https://mvnrepository.com/artifact/org.springframework.cloud/spring-cloud-starter-netflix-eureka-server -->
        <dependency>
          <groupId>org.springframework.cloud</groupId>
          <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
        </dependency>
        <!-- https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-test -->
        <dependency>
          <groupId>org.springframework.boot</groupId>
          <artifactId>spring-boot-starter-test</artifactId>
          <scope>test</scope>
        </dependency>
      </dependencies>
      <dependencyManagement>
        <dependencies>
          <!-- https://mvnrepository.com/artifact/org.springframework.cloud/spring-cloud-dependencies -->
          <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-dependencies</artifactId>
            <version>2023.0.1</version>
            <type>pom</type>
            <scope>import</scope>
          </dependency>
        </dependencies>
      </dependencyManagement>
      <build>
        <finalName>DiscoveryService</finalName>
        <plugins>
          <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
          </plugin>
        </plugins>
      </build>
   ```
3. Run the application. Go to localhost and we can the representation of DiscoveryService.

   <img width="1438" alt="Screenshot 2024-07-13 at 9 27 52 AM" src="https://github.com/user-attachments/assets/cb3f8bf1-0398-41a7-9e9b-9e511e9e6526">

   <img width="879" alt="Screenshot 2024-07-13 at 9 30 42 AM" src="https://github.com/user-attachments/assets/0502de50-2143-4f08-8537-ebb76f52fba5">
   <img width="961" alt="Screenshot 2024-07-13 at 9 30 56 AM" src="https://github.com/user-attachments/assets/e700329b-6d9d-4e58-8253-9eff0af64dfb">

   We can see some errors as well.

   <img width="1342" alt="Screenshot 2024-07-13 at 9 29 09 AM" src="https://github.com/user-attachments/assets/ff704a7c-35a6-4f1a-bb87-6da6369a3f4e">
   <img width="1353" alt="Screenshot 2024-07-13 at 9 29 16 AM" src="https://github.com/user-attachments/assets/56af5b6f-8f2c-4031-a0f9-f4270cc0bca6">

   Basically, it tries to connect to the URL mentioned. "8761" is the default port number for Eureka. "/eureka/" is the base URL for all our eureka Rest API calls.
   Our Discovery Service tries to connect to this and fetch some information.

   <img width="1066" alt="Screenshot 2024-07-13 at 10 08 20 AM" src="https://github.com/user-attachments/assets/5a992e92-b1b6-4d7a-a609-86da5c203456">
   <img width="742" alt="Screenshot 2024-07-13 at 10 09 02 AM" src="https://github.com/user-attachments/assets/68853aa9-b194-4234-b5f6-bce26176623f">

   Our Eureka Server assumes that we have another Eureka Server running on port 8761 that has a service registry. So in regular intervals, it pings the Eureka server at 8761 to check
   if there's any update in the registry.

   <img width="789" alt="Screenshot 2024-07-13 at 10 31 51 AM" src="https://github.com/user-attachments/assets/5191cbc7-3b34-4a9e-b451-ff2a43a27767">

   Currently, in our case, we don't have any other Eureka Server running on 8761 so we keep getting the same error message at regular time intervals for reasons mentioned above.

   <img width="962" alt="Screenshot 2024-07-13 at 10 20 43 AM" src="https://github.com/user-attachments/assets/01adc8ba-4898-4614-a92c-60581972bb8d">

   ------------------
   #### Note
   
   If we change port no to something else other than the default, we need to mention it in the properties file so that "registering itself" can work properly.

   <img width="872" alt="Screenshot 2024-07-13 at 12 10 03 PM" src="https://github.com/user-attachments/assets/3740814c-6298-4e9a-80e7-05efbbd0d6aa">

   <img width="1149" alt="Screenshot 2024-07-13 at 12 15 12 PM" src="https://github.com/user-attachments/assets/3feb5c18-fee1-4c6f-b5d6-f4cf34af3bbe">
   <img width="911" alt="Screenshot 2024-07-13 at 12 14 57 PM" src="https://github.com/user-attachments/assets/04269492-9c13-45e3-8cac-aa238cc72521">

   If the hostname is same as the one present in URL, it never searches for the replica

   <img width="985" alt="Screenshot 2024-07-13 at 12 16 17 PM" src="https://github.com/user-attachments/assets/fd0e0190-b16f-4bbe-992c-3e601df3de31">

   #### The properties "fetch-registery" & "register-with-eureka" is by default true.

   <img width="1146" alt="Screenshot 2024-07-13 at 12 19 22 PM" src="https://github.com/user-attachments/assets/6e15ff3b-8665-4c06-8f03-cf25eb0f88cf">
   ------------------

   Service "C" added in Registry.

   <img width="994" alt="Screenshot 2024-07-13 at 10 20 58 AM" src="https://github.com/user-attachments/assets/7b631b51-f8c2-4d9a-86c2-e92a976d6285">

   Our Eureka Server pings and gets the updated Registry.

   <img width="1017" alt="Screenshot 2024-07-13 at 10 21 16 AM" src="https://github.com/user-attachments/assets/3b51a2ba-775f-4686-a9a4-a4d8ee2fbda1">

   If we don't have another Eureka Server, we can turn it off.

   <img width="990" alt="Screenshot 2024-07-13 at 10 28 40 AM" src="https://github.com/user-attachments/assets/2cef1caf-a589-40b0-b4d6-d76a074dc50e">

   For this, we need to tell Spring Boot that we have only 1 Discovery Server and there's no need to look for any other DiscoveryServer as of now.

   <img width="771" alt="Screenshot 2024-07-13 at 10 14 08 AM" src="https://github.com/user-attachments/assets/1f5cd1a5-beeb-4bab-9a68-3f361c6311bb">
   <img width="1101" alt="Screenshot 2024-07-13 at 10 29 34 AM" src="https://github.com/user-attachments/assets/37f37d49-e3b7-4803-897d-ffd88d5d12d5">
   <img width="1029" alt="Screenshot 2024-07-13 at 10 41 03 AM" src="https://github.com/user-attachments/assets/aebfee0a-2201-44a8-a072-bfddf91658a7">

   If we run now, there won't be any exceptions.

   <img width="1346" alt="Screenshot 2024-07-13 at 10 16 43 AM" src="https://github.com/user-attachments/assets/2c737286-1752-42de-8a10-f46ddd6b7757">
   <img width="1409" alt="Screenshot 2024-07-13 at 10 41 48 AM" src="https://github.com/user-attachments/assets/8a1d84b9-9d21-4862-a0df-b70e82d8feac">
   <img width="1168" alt="Screenshot 2024-07-13 at 10 42 33 AM" src="https://github.com/user-attachments/assets/22073bab-b8b9-4920-815e-e62f6fe3be4c">

   But we don't want our DiscoveryServiceApplication to be registered with Eureka.

   In that case, we can turn it off.

   <img width="967" alt="Screenshot 2024-07-13 at 10 43 55 AM" src="https://github.com/user-attachments/assets/f7409078-d5c6-4ffe-95c1-a8b185def046">
   <img width="1155" alt="Screenshot 2024-07-13 at 10 44 52 AM" src="https://github.com/user-attachments/assets/d4da2046-1b9d-4a1f-82a5-d28b9124b3ea">
