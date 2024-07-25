# Archetypes

We can create a simple project using archetype. These are used an template. Archetype can be defined as an original that can be imitated. It configures the project for us.

```
-> mvn archetype:generate -> spring-data-basic(artifact id) -> 1 -> provide group & artifactId.
```

## Create own archetype:mvn archetype:create-from-project

We can create a template project which can we used by other members of the organization and thus be standardized.

* Create a new project with command "*mvn archetype:generate*"
* Accept default archetype template (No 6)
* Provide groupId & artifactId for the new project
* Just for learning purpose, add a new class to distinguish our project as a litlle bit different
* To create this as an archetype, use command "*mvn archetype:create-from-project*". When we run this goal, it outputs the actual archetype in the project's target directory.
* Install this archetype to the local repository with "*mvn install*"
* Create a new project with "*mvn archetype:generate*"
* Provide archetype template name and choose 1
* Provide groupId, version and artifactIt of the new project
* The project is now built on top of the template archetype that was created earlier

## Multimodule projects

Post the below changes, we will be able to execute different maven commands on these projects as a whole. The command issued on the module base would hit both the modules.

<img width="1127" alt="Screenshot 2024-05-04 at 10 14 48 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/5c9e34c9-d3e4-44ee-a7f6-8f59ce377a7a">

## Additional features

When working with web applications, we need somewhere to deploy that web application too.

Tomcat is not a full blown J2EE application server. It is a servlet container. But it still allows us to deploy our applications/war file to a server.

* Download tomcat zip

# **TO BE CONTINUED**
