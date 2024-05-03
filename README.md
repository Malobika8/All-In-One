# Maven

It simplifies any of the jar based project by downloading dependencies. We can create a jar or war file from a Java project but maven automates the process.
Maven is a project under the Apache Software Foundation umbrella. It came into existence in 2003. It is primarily a Java tool. 
- Build tool: Creates deployable artifacts from source code. Automated/repeatable builds. Deploying artifacts on servers.
- Dependency management tool: Download project dependencies from centralized repositories. Automatically resolve the libraries required by project dependencies. Dependency scoping.
- Project management tool: Artifact versioning. Change logs. Documentation. Javadocs. Reports(Code coverage etc).
- Standard approach to build software: Consistent path for all projects. Convention over configuration.
- Primarily a command line tool

# ***Different components of maven***:

**Project Object Model**
- Describes,configures and customizes a maven project
- Maven reads the pom.xml file to build the project
- Define the address for the project artifact using a coordinate system
- Specifies project information, plugins, goals, dependencies and profiles.

**Repositories**
- Holds build artifacts and dependencies of varying types
- Local repositories(local cache)
- Remote repositories (Repository is a collection of artifacts/dependencies)
- Local repositories take precedence during dependency resolution

**Plugins and goals**
- Plugin is a collection of goals. Ex: Compiler plugin
- Goals perform the actions in maven build
- All work is done via plugins and goals
- Called independently or as part of a lifecycle phase

**Lifecycle and Phases**
- Lifecycle is a sequence of named phase
- Phases are executed sequentially
- 3 lifecycles:clean, default, site
- Executing a phase executes all previous phases

<img width="1010" alt="Screenshot 2024-05-02 at 10 39 29 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/edb3f009-424f-446e-99f0-3ace91c4a1c1">

- "project" tag is the root tag of every pom.xml file
- "<groupId>" unique id of the org
- under development: snapshot
- released: release
- "<packaging>" tells what type of package it will be. By default, its a jar
- mvn package: creates a jar file that contains the content of the project
- "<name>": informal name of the project (in place of official artifact name)
- "<description>": used to describe the project
- "<url>": If there's any url for more info
- "<organization><name></name></organization>": used to specify who is behind the project
- "<developers><developer><name></name><email></email></developer></developers>": used to mention the developers of the project
- Maven provides a way to take all the information provided in pom and build a site for it. This can be done with "mvn site". Go to target->site->index.html
- Maven's standard directory layout. The files,configs,resources etc are supposed to be as per the directory layout. This is basically convention over configuration. This is 
  essentially how maven knows where the .class files can be located
- The directory structure can be conigured and changed. However, its not recommended to do so in case of new projects. For legacy projects, it may be done. This can be configured using
  <build><sourceDirectory></sourceDirectory><directory></directory></build> tags.
- To see child pom and inherited pom(parent), type "mvn help:effective-pom
- To build one pom that inherits another pom:
  <img width="1145" alt="Screenshot 2024-05-03 at 10 25 09 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/9bfd814f-82e3-4180-bef6-f75eaa84fe45">
- mvn install: build our project and puts it in the local repository
- Maven "<Profile>" allows us to build our project for different environments like dev,eng etc. It provides us the provision to customize our build as per the environment.
  After creating a profile, the same can be run with "mvn -P<profile_id> package". However, we don't want to define the profile we would like to apply by using that command line flag 
  when we execute the goal. Sometimes it's not possible to specify that flag. Maven provides us a mechanism to take other environment characteristics into consideration when we 
  determine which profile to apply. This is known an activator. It checks something similar to the environment value and determine what profile to apply based on the value.
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
  
 - While the setup can be done manually, there's a plugin that can quickly set things up for us. Archetype is like a template that can be used with "mvn archetype:generate". We can   
   just press enter if we want to use the basic template.
   Ex: maven-archetype-quickstart
- "mvn eclipse:eclipse" turns a project into an eclipse project

# **Dependency Management**
Dependency management is pulling in the dependencies that is required for the project from a repository. It reduces the complexity of our work helps manage better.

- To pull down the dependencies: "mvn dependency:copy-dependencies"
- The local repository acts as a cache
- How does maven know which repository to pull dependencies from? It pull in from the repositories mentioned in pom under "<repositories>" tag
  <img width="1082" alt="Screenshot 2024-05-03 at 5 24 17 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/be62e028-c97c-4273-b86e-dd993c58d60a">
- If a repo is used extensively, it can be added in Settings.xml present inside the Apache Maven folder.
  <img width="1139" alt="Screenshot 2024-05-03 at 5 31 35 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/f9a588f0-eb5e-4e97-bf59-fdb14b1dddb3">
- The default scope for every dependency is compile
- The debug option can be enabled by specifying "mvn -X compile" before our phase. If a dependency scope is compile, it will be added to the classpath as can be checked by enabling 
  bug flag, "-X"
- To execute test phase with the bug flag specified: "mvn -X test"
- The "provided" scope is when we expect the dependency to be provided by something like the jdk or the container we're using. The dependency will be available for build and test phases by once the jar application is deployed, those dependencies won't be available withing that package
- A runtime dependency is not used for compilation. However, it would be ok to declare a runtime dependency as compile time dependency
- "system" scope makes the project very rigit. It pull in the dependencies from a filesystem. Whwn the project is run on another machine, the file system path might be different.

# **How to resolve conflicts between transitive dependencies?**
- When a project includes a dependency which includes two dependencies. Both the dependencies how include another dependency which is same but the version is different. In that case, 
  when we compile with debug flag enabled, it can be found that only one of the versions is pulled in.
  <img width="1100" alt="Screenshot 2024-05-03 at 5 59 00 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/3acd42f0-cdf5-4246-98f6-4a461ff82556">
  <img width="1102" alt="Screenshot 2024-05-03 at 5 59 15 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/a106c4bb-e67c-4fdd-91ec-ad71c4bead8d">
  <img width="1103" alt="Screenshot 2024-05-03 at 5 59 38 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/0147bb11-2ada-4c15-900e-fdcd769f011e">
  <img width="1111" alt="Screenshot 2024-05-03 at 6 00 39 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/c8bd7106-6117-46d2-af5d-514bf3756971">

  **What if we absolutely had to have version 3.0 included into our project?**
  Maven provided a mechanism that allows us to specify a dependency or an artifact should be excluded and that will cause the earlier version to be included in our project.
  <img width="1131" alt="Screenshot 2024-05-03 at 6 06 18 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/326a4382-e686-409e-be32-6e9abea19f58">
  <img width="1119" alt="Screenshot 2024-05-03 at 6 07 50 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/be4ce93e-668d-4654-ba92-8dc6d171a0c8">

# **Maven build lifecycle and plugins**
- A lifecycle helps us when we build test and distribute artifacts. It consists of a set of steps or stages that we go through as we build our artifact. These stages/steps are     
  referred to as phases. Within maven, there are 3 built in lifecycles **(default, clean & site)**. These individual lifecycles have their own particular phases. A goal binds to a   
  particular phase. A goal is essentially an action to be taken.
- "Default" lifecycles has 23 phases. Important phases:
  1) Compile phase: Compiles the source code of the project
  2) Test-compile: Compiles the test source code into the test destination directory
  3) Test: Runs test using a suitable unit testing framework. These tests should not require the code to be packaged or deployed.
     <img width="1053" alt="Screenshot 2024-05-03 at 9 29 15 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/78a15b69-427c-46af-9238-72499ada7740">
  4) Package: Take the compiled code and package it in its distributable format, such as a jar,ear,war.
  5) Install: Install the package into the local repository, for use as a dependency in other projects locally.
  6) Deploy: deploy in an Integration  or release environment, copies the final package to the remote repository for sharing with other developers and projects. Its about working in        crossed environments.
 
 # **Goals and plugins**
  - Goals perform tasks and those tasks are run against our project in order for something to happen. Plugins are comprised of a number of goals. Goal could be analogous to method and     plugins to class.
  - Syntax for executing a plugin: "mvn <nameOfThePlugin>:<goal>". Ex. "mvn compiler:compile"
  - Where these plugins come from? : In our pom.xml, the plugins are not specified. Then where does it come from? It comes from the super pom which can be confirmed by taking a look       at the effective pom. PluginRepositories are very similar to dependency repositories. We get a lot of default plugins from the same when working with plugin. Along with it, there      are basic 4 plugins generally listed in maven super-pom.

    <img width="1032" alt="Screenshot 2024-05-03 at 9 42 35 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/e6dbeb87-94e1-4620-9ff6-2ca851111e49">
    <img width="1075" alt="Screenshot 2024-05-03 at 9 44 50 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b0ca6372-4f6d-4ea0-9ece-ae6c8ea1b023">
    
    More info related to the working of plugin can found as
    <img width="1125" alt="Screenshot 2024-05-03 at 9 46 53 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/ac657719-7618-43dd-a7c8-0da32b126ca9">
    <img width="1093" alt="Screenshot 2024-05-03 at 9 49 23 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/fd1e418f-07c7-43f5-9d15-28ef49014e9a">

  
<img width="1067" alt="Screenshot 2024-05-02 at 6 00 34 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/3bdcaeb3-f753-4733-b5b5-e17575e705cd">
<img width="1067" alt="Screenshot 2024-05-02 at 6 01 57 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/60bf72a4-be7c-4a67-bf7e-6dfdc06a0efb">

**Maven installation in Mac**
- Go to Terminal
- Type "brew install maven"
- Check if it's installed correctly by checking "mvn --version"
**Note**: To uninstall - "brew uninstall maven"

<img width="1004" alt="Screenshot 2024-05-02 at 6 11 49 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/c73b78b6-31ad-4260-84e4-e8baf603d13d">
<img width="1020" alt="Screenshot 2024-05-02 at 6 12 53 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/85356f9b-66a6-4670-8bea-39044fbb659a">
<img width="1090" alt="Screenshot 2024-05-02 at 6 31 28 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/886ace01-4fd1-4b9a-be76-a2e17a017e4b">
<img width="1039" alt="Screenshot 2024-05-02 at 6 32 07 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b2d1ec67-2f6b-49a7-abe7-f85703fb225a">
<img width="1020" alt="Screenshot 2024-05-02 at 6 32 14 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/9704e879-27a9-4632-95a2-7474d5911bb2">
<img width="1015" alt="Screenshot 2024-05-02 at 6 32 45 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/8416c429-1d92-4a3a-b2cf-ece9969a2798">
<img width="1067" alt="Screenshot 2024-05-02 at 6 34 05 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/7f034de3-95ef-4627-8e12-e093823bc16f">
<img width="1046" alt="Screenshot 2024-05-02 at 6 35 16 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b7b47f3e-0819-44c6-a4ce-3147fa0a6337">
<img width="1059" alt="Screenshot 2024-05-02 at 6 36 58 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/1f1f4877-0161-4677-a99e-1b7ce93d0c3b">
<img width="1078" alt="Screenshot 2024-05-02 at 6 35 44 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/c36c205f-2f2a-497b-b053-6da84a4f31ad">
<img width="1077" alt="Screenshot 2024-05-02 at 6 37 54 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/c87a3d88-2a98-45cb-bb6c-8c349df636af">
<img width="1064" alt="Screenshot 2024-05-02 at 6 38 34 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/1f8b6a0e-44e0-462f-9bce-86fb36d69d29">
<img width="995" alt="Screenshot 2024-05-02 at 6 39 22 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/d8cae7aa-ba95-46b1-81b2-8c5d2cb62fcb">
<img width="1059" alt="Screenshot 2024-05-02 at 6 40 28 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/8f76d866-3498-41be-86e8-baada713087e">
<img width="1060" alt="Screenshot 2024-05-02 at 6 40 56 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/58ea3b8f-757d-4ac5-9470-ede68912e752">
<img width="1056" alt="Screenshot 2024-05-02 at 6 42 22 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/8eecd8de-9faf-488f-8d60-a2a25ebea3fe">
<img width="1061" alt="Screenshot 2024-05-02 at 6 43 10 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/764a764d-7954-4ef0-86fe-60973aa585d8">

  
