# Maven Custom plugin

Plugin that a user can develop for a particular need. We need to have a basic create archetype which can be created by the following command

<img width="854" alt="Screenshot 2024-05-04 at 10 13 05 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/1fb2c5be-03e0-4fc2-9702-7edfca637533">

-> Then do "*mvn install*"

* ### Long way of referring our plugin:
  - Add groupId artifactId and touch goal of Maven custom compiler to other project - 

    ```
    "mvn org.example:MavenCustomPlugin:touch" 
    
    i.e. "mvn <groupId>:<artifactId>:goal"
    ```
    
  - When we refresh the other project, we see touch.txt created in target folder

* ### Concise way of referring our plugin:
  - Navigate to pom.xml file of the first custom project
  - To allow us to use prefix for our plugin instead of group and artifactId so that we can reference it in short way
  - add this in pom.xml of Custom plugin project

    ```
      <build>
      <plugins>
      <plugin>
        <artifactId>maven-plugin-plugin</artifactId>
        <version>2.3</version>
        <configuration>
          <goalPrefix>customPlugin</goalPrefix>
        </configuration>
      </plugin>
      </plugins>
      </build>
    ```

  - Head to pom.xml of the second project and add

    ```
      <build>
        <plugins>
            <plugin>
                <groupId>org.example</groupId> <!-- coordinates of custom plugin project-->
                <artifactId>MavenCustomPlugin</artifactId>
                <version>1.0-SNAPSHOT</version>

                <executions>
                    <execution>
                        <id>first-custom-compile</id> <!--execution id-->
                        <phase>compile</phase> <!-- bind it to an execution phase-->
                        <goals>
                            <goal>touch</goal> <!--goal that we would like to execute in this phase-->
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
      </build>
    ```
    
  - We have now setup of custom plugin that we want to use in the target project
  - To run custom plugin within our target project: "*mvn <pluginPrefix>:<goal>*"

    ```
    eg: mvn customPlugin:touch
    ```

# Goals and Plugins

To know more about different available plugins, check https://maven.apache.org/plugins/

1) ### Clean Plugin
   
   Clears the target directory. It is generally executed when we're starting over. The clean plugin only has one goal
   ```
   "mvn clean:clean"
   ```
   
2) ### Jar Plugin
   
   It's a core maven plugin and is used to build a jar file from our current project. The plugin also allows us to build a jar from our test classes.
   
   Invoke using package phase "*mvn package*"
   
   Can also explicitely be invoked using jar plugin and jar goal.

   ```
   "mvn jar:jar"
   ```
   
   #### How to specify parameters when creating jar files?
   
   Add parameter to have a jar name and force the creation of jar each time.

   ```
   "mvn jar:jar -Djar.finalName=test -Djar.forceCreation=true"
   ```
   
   #### Where to look for parameters that can be specified with goals?
   
   Go to individual plugin goals -> https://maven.apache.org/plugins/maven-jar-plugin/jar-mojo.html
   
   #### How to do the same by modifying pom?
   
   Go to build->pluginManagement and add in the configuration section
   
   <img width="818" alt="Screenshot 2024-05-04 at 11 25 11 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/edd37fa0-0860-481e-8ecc-0ca62919991f">

   ```
   Do mvn clean compile jar:jar
   ```
   
   <img width="268" alt="Screenshot 2024-05-04 at 11 25 25 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/fd49b3ef-9be4-4c06-9901-f3752c015452">
   
3) ### Javadoc Plugin
   
   The plugin allows us to create javadocs for projects which describes the API

   ```
   eg: mvn javadoc:javadoc (Command line)
   ```
   
   Updating in pom
   
   <img width="924" alt="Screenshot 2024-05-04 at 11 47 15 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/5417e5d4-ff86-4498-9291-e9b644c8147e">

   #### Note : When to put inside pluginManagement and when to put simply in plugins?
   
   When the plugin is already declared in super pom and we just need to modify on top of it, pluginManagement is used.
   When the plugin is not declared in super pom, we need to first declare it in our pom.xml which is why we have to add it in plugins tab. Then we can add configuration inside the
   pluginManagement tab.

4) ### Install and deploy plugin
   
  These are two plugins that help us distribute maven artifact we have built.
  
  * Install plugin takes the artifact we have built and installs it in the local repository. Once in the repository, other maven projects can consume the same.
  * Deploy plugin is meant to take an artifact and deploy it to a remote repository. A lot of times organization creates their own maven repository. There are things like "mavencentral"     that are shared amongst many individuals, people working in diff orgs, casual developers. The deploy plugin or deploy goal ships out our artifact to one of those remote                repositories.
    We need to setup repository details in pom i.e where to send the artifacts. There are configuration that we need to put in place in order to deploy to the targeted repository.
    
        <distributionManagement>
        <repository>
            <id>testRepositoryId</id>
            <name>maven-remote</name>
            <url>https://repo1.maven.org/maven2</url>
        </repository>
        </distributionManagement>
    
5) ### Surefire plugin
   
  Integrates test driven development. 
  ```
  "mvn test"
  ```
6) ### War plugin
   
  mvn package will invoke maven war plugin or directly "*mvn war:war*" can be used
