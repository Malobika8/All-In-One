# Dependency Management

Dependency management is pulling in the dependencies that is required for the project from a repository. It reduces the complexity of our work helps manage better.

- To pull down the dependencies: "*mvn dependency:copy-dependencies*"
- The local repository acts as a cache
  
- #### How does maven know which repository to pull dependencies from?
  
  It pull in from the repositories mentioned in pom under "repositories" tag
  
  <img width="1082" alt="Screenshot 2024-05-03 at 5 24 17 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/be62e028-c97c-4273-b86e-dd993c58d60a">
  
- If a repo is used extensively, it can be added in Settings.xml present inside the Apache Maven folder.
  
  <img width="1139" alt="Screenshot 2024-05-03 at 5 31 35 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/f9a588f0-eb5e-4e97-bf59-fdb14b1dddb3">
  
- The default scope for every dependency is compile
- The debug option can be enabled by specifying "*mvn -X compile*" before our phase. If a dependency scope is compile, it will be added to the classpath as can be checked by enabling 
  bug flag, "*-X*"
- To execute test phase with the bug flag specified: "*mvn -X test*"
- The "provided" scope is when we expect the dependency to be provided by something like the jdk or the container we're using. The dependency will be available for build and test phases by once the jar application is deployed, those dependencies won't be available withing that package
- A runtime dependency is not used for compilation. However, it would be ok to declare a runtime dependency as compile time dependency
- "system" scope makes the project very rigit. It pull in the dependencies from a filesystem. When the project is run on another machine, the file system path might be different.

# How to resolve conflicts between transitive dependencies?

- When a project includes a dependency which includes two dependencies. Both the dependencies how include another dependency which is same but the version is different. In that case, 
  when we compile with debug flag enabled, it can be found that only one of the versions is pulled in.
  
  <img width="1100" alt="Screenshot 2024-05-03 at 5 59 00 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/3acd42f0-cdf5-4246-98f6-4a461ff82556">
  <img width="1102" alt="Screenshot 2024-05-03 at 5 59 15 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/a106c4bb-e67c-4fdd-91ec-ad71c4bead8d">
  <img width="1103" alt="Screenshot 2024-05-03 at 5 59 38 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/0147bb11-2ada-4c15-900e-fdcd769f011e">
  <img width="1111" alt="Screenshot 2024-05-03 at 6 00 39 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/c8bd7106-6117-46d2-af5d-514bf3756971">

  ### What if we absolutely had to have version 3.0 included into our project?
  
  Maven provided a mechanism that allows us to specify a dependency or an artifact should be excluded and that will cause the earlier version to be included in our project.
  
  <img width="1131" alt="Screenshot 2024-05-03 at 6 06 18 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/326a4382-e686-409e-be32-6e9abea19f58">
  <img width="1119" alt="Screenshot 2024-05-03 at 6 07 50 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/be4ce93e-668d-4654-ba92-8dc6d171a0c8">


  
