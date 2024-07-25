# Maven working

<img width="1010" alt="Screenshot 2024-05-02 at 10 39 29 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/edb3f009-424f-446e-99f0-3ace91c4a1c1">

- "project" tag is the root tag of every pom.xml file
- "groupId" unique id of the org
- under development: snapshot
- released: release
- "packaging" tells what type of package it will be. By default, it's a jar.
- *mvn package*: creates a jar file that contains the content of the project
- "name": informal name of the project (in place of official artifact name)
- "description": used to describe the project
- "url": If there's any url for more info
- Used to specify who is behind the project:

      <organization><name></name></organization>
  
- Used to mention the developers of the project:

      <developers><developer><name></name><email></email></developer></developers>
  
- Maven provides a way to take all the information provided in pom and build a site for it. This can be done with "mvn site".
  ```
  Go to target->site->index.html
  ```
- Maven's standard directory layout. The files,configs,resources etc are supposed to be as per the directory layout. This is basically convention over configuration. This is 
  essentially how maven knows where the .class files can be located.
- The directory structure can be configured and changed. However, it's not recommended to do so in case of new projects. For legacy projects, it may be done. This can be configured using

      <build><sourceDirectory></sourceDirectory><directory></directory></build> 
  
- To see child pom and inherited pom(parent), type "*mvn help:effective-pom*"
- To build one pom that inherits another pom:
  
  <img width="1145" alt="Screenshot 2024-05-03 at 10 25 09 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/9bfd814f-82e3-4180-bef6-f75eaa84fe45">
  
- *mvn install*: build our project and puts it in the local repository
- Maven "Profile" allows us to build our project for different environments like dev,eng etc. It provides us the provision to customize our build as per the environment.
  After creating a profile, the same can be run with
  ```
  mvn -P<profile_id> package
  ```
  However, we don't want to define the profile we would like to apply by using that command line flag when we execute the goal. Sometimes it's not possible to specify that flag. Maven
  provides us a mechanism to take other environment characteristics into consideration when we determine which profile to apply. This is known an activator. It checks something similar
  to the environment value and determine what profile to apply based on the value.
  
  <img width="1116" alt="Screenshot 2024-05-03 at 11 15 16 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/bc417ddc-4768-4d1c-87be-74dda0990a4c">

      <profiles>
            <profile>
                <id>production</id>
                <activation>
                    <property>
                        <name>env.PACKAGE_ENV</name>
                        <value>PROD</value>
                    </property>
                </activation>
                <build>
                    <directory>Production</directory>
                </build>
            </profile>
      </profiles>
  
 - While the setup can be done manually, there's a plugin that can quickly set things up for us. Archetype is like a template that can be used with
   ```
   mvn archetype:generate"
   ```
   We can just press enter if we want to use the basic template.
   ```
   Ex: maven-archetype-quickstart
   ```
- *mvn eclipse:eclipse*: turns a project into an eclipse project

