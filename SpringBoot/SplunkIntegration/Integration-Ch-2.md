# Splunk Integration with a SpringBoot project

1. Open any existing SpringBoot project.
2. Include log4j & exclude default logging that SpringBoot provides.

   Exclude spring boot logging.
  
   ```
   <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-web</artifactId>
      <exclusions>
        <exclusion>
          <groupId>org.springframework.boot</groupId>
          <artifactId>spring-boot-starter-logging</artifactId>
        </exclusion>
      </exclusions>
    </dependency>
   ```

   Include log4j

   ```
   <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-log4j</artifactId>
   </dependency>
   ```

   We might come across an error.

   <img width="1398" alt="Screenshot 2024-07-28 at 10 36 22 AM" src="https://github.com/user-attachments/assets/173a37cd-04a8-4f19-96db-f6428d225380">

   Include log4j2.

   ```
   <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-log4j2</artifactId>
   </dependency>
   ```

3. Add logs to the project.

   <img width="999" alt="Screenshot 2024-07-28 at 10 43 38 AM" src="https://github.com/user-attachments/assets/cc6df0a0-c649-49c2-802b-89dfcc2a8b51">
   <img width="1037" alt="Screenshot 2024-07-28 at 10 46 03 AM" src="https://github.com/user-attachments/assets/a1df89fa-bb19-4149-9cff-02476f007d8d">
   <img width="979" alt="Screenshot 2024-07-28 at 10 48 54 AM" src="https://github.com/user-attachments/assets/1a5e6bde-342a-4706-b5d1-2a121f496dbc">

4. Integrate with Splunk.

   Check out the documentation - https://dev.splunk.com/enterprise/docs/devtools/java/logging-java/getstartedloggingjava/installloggingjava/

   Add dependencies:

   ```
   <repositories> 
        <repository> 
            <id>splunk-artifactory</id> 
            <name>Splunk Releases</name> 
            <url>https://splunk.jfrog.io/splunk/ext-releases-local</url> 
        </repository>
   </repositories>
   ```
   ```
    <dependency>
          <groupId>com.splunk.logging</groupId>
          <artifactId>splunk-library-javalogging</artifactId>
          <version>1.8.0</version>
          <scope>runtime</scope>
    </dependency>
    ```

    Create Splunk logging configuration. Copy token value created, index, source type, source name. (We can get all these details from the newly
    created Splunk index)

    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <Configuration>
    <Appenders>
        <Console name="console" target="SYSTEM_OUT">
            <PatternLayout
                    pattern="%style{%d{ISO8601}} %highlight{%-5level }[%style{%t}{bright,blue}] %style{%C{10}}{bright,yellow}: %msg%n%throwable" />
        </Console>
        <SplunkHttp
                name="splunkhttp"
                url="http://localhost:8088"
                token="888dce00-cd58-42e0-b03f-38da61b81a42"
                host="localhost"
                index="spring_dev"
                type="raw"
                source="source name"
                sourcetype="log4j"
                messageFormat="text"
                disableCertificateValidation="true">
            <PatternLayout pattern="%m" />
        </SplunkHttp>

    </Appenders>

    <Loggers>
        <Root level="info">
            <AppenderRef ref="console" />
            <AppenderRef ref="splunkhttp" />
        </Root>
    </Loggers>
    </Configuration>
    ```

5. Run the Application and do some operations.
6. Check in Splunk for logs.

   Untick "Enable indexer acknowledgement"

   <img width="809" alt="Screenshot 2024-07-28 at 12 05 11 PM" src="https://github.com/user-attachments/assets/aaba99c1-930d-4ffe-9592-c255cadfdc0d">

   We need to search with the name of our index created.

   ```
   index="spring_dev"
   ```

    

   

    






   
