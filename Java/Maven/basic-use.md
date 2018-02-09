# Basic Maven Usage

* [Spring's Maven Guide is a great generic introduction to Maven](https://spring.io/guides/gs/maven/)
  * Covers using dependencies, tests, typical commands, packaging
* [Maven's 5 minute guide](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html)

Generate a default project with a `groupdId`, `artifactId`, and optionally `version` with the quickstart archetype like so: `mvn archetype:generate -DgroupId=com.joshdoug.app -DartifactId=hello -Dversion=0.0.1 -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`, replace examples as appropiate. This will create a project with the standard project structure. Alternatively `mvn archetype:generate` can be used which is interactive. This will automatically include JUnit as a dependency (version 3.8.1?!).

Alternatively use a basic POM and set up the directory structure manually, POM example:

```XML
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.joshdoug.hello</groupId>
    <artifactId>Hello</artifactId>
    <packaging>jar</packaging>
    <version>0.1.0</version>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-shade-plugin</artifactId>
                <version>3.1.0</version>
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>shade</goal>
                        </goals>
                        <configuration>
                            <transformers>
                                <transformer
                                    implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                                    <mainClass>com.joshdoug.hello.HelloWorld</mainClass>
                                </transformer>
                            </transformers>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</project>
```

This pom adds the `maven-shade-plugin` so that the project can be packaged up into a single 'uber' jar containing any dependencies as well. The packaging element could also be `war`, as well as other less used alternatives.

For setting up the directory structure manually, see the [introduction to the Standard Directory Layout](https://maven.apache.org/guides/introduction/introduction-to-the-standard-directory-layout.html).

Additions to the POM that may be necessary:

```XML
<properties>
    <maven.compiler.source>9</maven.compiler.source>
    <maven.compiler.target>9</maven.compiler.target>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
</properties>
```

This set the compiler version manually, otherwise Maven has a strange habit of defaulting to 1.5...which it doesn't support. This also sets the encoding to avoid the 'build is platform dependent' warning message.

With a basic hello world, this can now be compiled, packaged, installed, and run.

* `mvn compile` will simply compile the class(es)
* `mvn package` will package it into a jar (or war), it will also compile it first and run any tests
* `mvn install` will add the jar to the local maven cache (`.m2`), this will also compile, run tests, and package the project

## Adding dependencies

Just add the dependencies to the pom as normal, example:

```XML
<dependencies>
    <dependency>
        <groupId>joda-time</groupId>
        <artifactId>joda-time</artifactId>
        <version>2.9.9</version>
    </dependency>
</dependencies>
```

Here joda-time provides an alternative Time library to use.

Dependency scopes:

* `compile` - the default scope, they should be available at compile-time
* `provided` - dependencies that are required for compiling the project code, but will be provided at runtime by a container running the code (e.g. the Java Servlet API)
* `test` - used for compiling and running tests, but not required for building or running the project's runtime code