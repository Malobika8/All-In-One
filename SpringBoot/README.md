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
