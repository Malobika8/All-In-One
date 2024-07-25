# Maven
It simplifies any of the jar-based projects by downloading dependencies. We can create a jar or war file from a Java project but Maven automates the process.

Maven is a project under the Apache Software Foundation umbrella. It came into existence in 2003. It is primarily a Java tool. 

- Build tool: Creates deployable artifacts from source code. Automated/repeatable builds. Deploying artifacts on servers.
- Dependency management tool: Download project dependencies from centralized repositories. Automatically resolve the libraries required by project dependencies. Dependency scoping.
- Project management tool: Artifact versioning. Change logs. Documentation. Javadocs. Reports(Code coverage etc).
- Standard approach to building software: Consistent path for all projects. Convention over configuration.
- Primarily a command line tool

# Different components of maven

## Project Object Model 
- Describes,configures and customizes a maven project
- Maven reads the pom.xml file to build the project
- Define the address for the project artifact using a coordinate system
- Specifies project information, plugins, goals, dependencies and profiles.

## Repositories
- Holds build artifacts and dependencies of varying types
- Local repositories(local cache)
- Remote repositories (Repository is a collection of artifacts/dependencies)
- Local repositories take precedence during dependency resolution

## Plugins and goals
- Plugin is a collection of goals. Ex: Compiler plugin
- Goals perform the actions in maven build
- All work is done via plugins and goals
- Called independently or as part of a lifecycle phase

## Lifecycle and Phases
- Lifecycle is a sequence of named phase
- Phases are executed sequentially
- 3 lifecycles:clean, default, site
- Executing a phase executes all previous phases
