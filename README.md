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

- "<project>" tag is the root tag of every pom.xml file
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

  
