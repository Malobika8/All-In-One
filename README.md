<img width="932" alt="Screenshot 2025-07-09 at 11 09 00 PM" src="https://github.com/user-attachments/assets/8d750f18-4a87-4f96-af44-30f6af2a737f" />

# Microservices using Java + Spring Boot

<img width="1207" alt="Screenshot 2024-07-10 at 7 19 11 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/5eb17914-7edc-4454-be2a-2fdbeda3d7d5">
<img width="744" alt="Screenshot 2024-07-10 at 7 20 12 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/3c555a85-7b9e-4704-b000-9b28c9491d62">
<img width="1099" alt="Screenshot 2024-07-10 at 7 20 05 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/6c7f2af6-12bd-4e80-b142-7cf44da48f62">
<img width="1185" alt="Screenshot 2024-07-10 at 7 21 08 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9179f8a2-b38b-421e-99a8-3a8699df57b9">

# FYI

By default, Spring Boot repackages your JAR into an executable JAR, and it does that by putting all of your classes inside BOOT-INF/classes, and all of the dependent libraries inside BOOT-INF/lib. The consequence of creating this fat JAR is that you can no longer use it as a dependency for other projects.

From Custom repackage classifier:

By default, the repackage goal will replace the original artifact with the repackaged one. That's same behavior for modules that represent an app but if your module is used as a dependency of another module, you need to provide a classifier for the repackaged one.

The reason for that is that application classes are packaged in BOOT-INF/classes so that the dependent module cannot load a repackaged jar's classes.

If you want to keep the original main artifact in order to use it as a dependency, you can add a classifier in the repackage goal configuration:

```
<plugin>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-maven-plugin</artifactId>
  <version>1.4.1.RELEASE</version>
  <executions>
    <execution>
      <goals>
        <goal>repackage</goal>
      </goals>
      <configuration>
        <classifier>exec</classifier>
      </configuration>
    </execution>
  </executions>
</plugin>
```

For SpringBoot 3, we can just use

```
<plugin>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-maven-plugin</artifactId>
  <version>1.4.1.RELEASE</version>
  <executions>
    <execution>
      <goals>
        <goal>repackage</goal>
      </goals>
    </execution>
  </executions>
</plugin>
```

With this configuration, the Spring Boot Maven Plugin will create 2 JARs: the main one will be the same as a usual Maven project, while the second one will have the classifier appended and be the executable JAR.
