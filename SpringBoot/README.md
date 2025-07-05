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


## 💡 What is a **Fat JAR** in Spring Boot?

A **fat JAR** is a **JAR file that contains your application code AND all its dependencies** bundled inside it — so it's self-contained.

✅ **You can run it directly** with just one command:

```bash
java -jar myapp.jar
```

---

## 🔍 Why “Fat”?

Because unlike a normal JAR (which only contains your classes), a fat JAR also includes:

* All Spring Boot dependencies
* All third-party libraries (like Jackson, Logback, etc.)
* Embedded server (like Tomcat or Jetty)
* Your compiled `.class` files

That makes the JAR **“fat”** — it carries everything it needs to run.

---

## 📦 Example: Fat JAR Structure

```
myapp.jar
├── BOOT-INF/
│   ├── classes/        <-- Your compiled Java classes
│   └── lib/            <-- All dependencies (Spring Boot, DB drivers, etc.)
├── META-INF/
└── org/springframework/boot/loader/  <-- Spring Boot launcher
```

---

## 🛠️ How It's Created (Using Maven)

If you're using Maven:

```xml
<build>
  <plugins>
    <plugin>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-maven-plugin</artifactId>
    </plugin>
  </plugins>
</build>
```

Then run:

```bash
mvn clean package
```

It will generate a fat JAR in:

```
target/myapp-0.0.1-SNAPSHOT.jar
```

You can now run it:

```bash
java -jar target/myapp-0.0.1-SNAPSHOT.jar
```

---

## ✅ Benefits of Fat JAR

| Feature                  | Explanation                            |
| ------------------------ | -------------------------------------- |
| ✔ Self-contained         | No need to install Tomcat separately   |
| ✔ Easy deployment        | Just copy the `.jar` to server and run |
| ✔ Works anywhere Java is | Portable                               |
| ✔ Dev-friendly           | Fast development and testing           |

---

## ❗ Note:

* Spring Boot fat JAR **embeds Tomcat** (or Jetty/Undertow), so **you don’t need to deploy a WAR** to Tomcat.
* This is what makes Spring Boot different from traditional Java web apps.

---

