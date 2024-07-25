# Maven build lifecycle and plugins

- A lifecycle helps us when we build test and distribute artifacts. It consists of a set of steps or stages that we go through as we build our artifact. These stages/steps are     
  referred to as phases. Within maven, there are 3 built in lifecycles **(default, clean & site)**.

  These individual lifecycles have their own particular phases. A goal binds to a particular phase. A goal is essentially an action to be taken.
  
- "Default" lifecycles has 23 phases.

  Important phases:
  - Compile phase: Compiles the source code of the project
  - Test-compile: Compiles the test source code into the test destination directory
  - Test: Runs test using a suitable unit testing framework. These tests should not require the code to be packaged or deployed.
    
     <img width="1053" alt="Screenshot 2024-05-03 at 9 29 15 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/78a15b69-427c-46af-9238-72499ada7740">
     
  - Package: Take the compiled code and package it in its distributable format, such as a jar,ear,war.
  - Install: Install the package into the local repository, for use as a dependency in other projects locally.
  - Deploy: deploy in an Integration  or release environment, copies the final package to the remote repository for sharing with other developers and projects. Its about working in        crossed environments.
 
 # Goals and plugins
  - Goals perform tasks and those tasks are run against our project in order for something to happen. Plugins are comprised of a number of goals. Goal could be analogous to method and     plugins to class.
  - Syntax for executing a plugin:

        "mvn <nameOfThePlugin>:<goal>".

    Ex. "mvn compiler:compile"
    
  - #### Where these plugins come from?
  
    In our pom.xml, the plugins are not specified. Then where does it come from? It comes from the super pom which can be confirmed by taking a look at the effective pom.
    PluginRepositories are very similar to dependency repositories. We get a lot of default plugins from the same when working with plugin. Along with it, there are basic 4 plugins
    generally listed in maven super-pom.

    <img width="1032" alt="Screenshot 2024-05-03 at 9 42 35 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/e6dbeb87-94e1-4620-9ff6-2ca851111e49">
    <img width="1075" alt="Screenshot 2024-05-03 at 9 44 50 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b0ca6372-4f6d-4ea0-9ece-ae6c8ea1b023">
    
    More info related to the working of plugin can found as
    
    <img width="1125" alt="Screenshot 2024-05-03 at 9 46 53 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/ac657719-7618-43dd-a7c8-0da32b126ca9">
    <img width="1093" alt="Screenshot 2024-05-03 at 9 49 23 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/fd1e418f-07c7-43f5-9d15-28ef49014e9a">
    
    There are a list of properties that can be set for goals.
    
    ## How to set a property?
    
    * Specify property using command line

      ```
      mvn compiler:compile -Dmaven.compiler.verbose=true
      mvn <plugin>:<goal> -D<User property name>=<boolean>
      ```
       
    * Specify propery using pom.xml (Add plugin we would like to adjust)

           <build>
           <pluginManagement>
            <plugins>
                <plugin>
                    <groupId>or.apache.maven.plugins</groupId>
                    <artifactId>maven-compiler-plugin</artifactId>
                    <version>3.2</version>
                    <configuration>
                        <verbose>true</verbose>
                    </configuration>
                </plugin>
            </plugins>
           </pluginManagement>
           </build>
