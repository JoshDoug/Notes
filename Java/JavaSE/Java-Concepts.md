# OO Patterns, General Java Concepts etc

Might extend to cover JVM, JRE, JDK usage and options.

Tutorials provided by Oracle:

* [Java Tutorials Learning Paths](https://docs.oracle.com/javase/tutorial/tutorialLearningPaths.html)
* [The Java Tutorials](https://docs.oracle.com/javase/tutorial/index.html)

Lots of overlap, not sure why there are two pages for basically the same thing.

POJO - Plain Old Java Object

* An object that has both attributes and behavior

JavaBean

* A simple POJO whose only behavior is getters and setters
* Must have a default nullable constructor to conform to the JavaBean specification

DTO - Data Transfer Object

* A JavaBean (kinda) that functions as a transport of data from one layer to another
* Doesn't need to have a nullable constructor...

DAO - Data Access Object

OSGi - Open Services Gateway Initiative

## Java Tutorials

* [Main tutorial page](https://docs.oracle.com/javase/tutorial/index.html)
* [JavaSE Docs](https://docs.oracle.com/javase/8/docs/)
* [JavaEE Docs](https://docs.oracle.com/javaee/7/index.html)

### [JavaFX Tutorials and Documentation](https://docs.oracle.com/javase/8/javase-clienttechnologies.htm)

## Java Properties

Setting Java version on mac:

```shell
export JAVA_HOME=`/usr/libexec/java_home -v '1/8*'`
```

or

```shell
export JAVA_HOME=`/usr/libexec/java_home -v 1.8.0_121`
```

See the java_home man page.

A rather subpar overview of JDK install on macOS: [here](https://docs.oracle.com/javase/8/docs/technotes/guides/install/mac_jdk.html).

More on Java Properties in Platform-Environment.md.

## Java Manifest

[Setting up the manifest.](https://docs.oracle.com/javase/tutorial/deployment/jar/manifestindex.html)

## Running from the CLI

Setting up and running a project from the command line (HelloWorld)
(Using the pre-Ant part of Ant's tutorial)

Create the project directory and files within it:

```shell
mkdir -pv HelloWorld/{build/{classes,jar},src/oata}
cd HelloWorld
```

Then create the HelloWorld java source file:

```shell
cat > src/oata/HelloWorld.java << "EOF"
package oata;

public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}
EOF
```

Test that it all compiles and runs:

```shell
javac -sourcepath src -d build/classes src/oata/HelloWorld.java
java -cp build/classes oata.HelloWorld
```

Then create the manifest file:

```shell
echo "Main-Class: oata.HelloWorld" > myManifest
```

Then create and run a jar of it:

```shell
jar cfm build/jar/HelloWorld.jar myManifest -C build/classes .
java -jar build/jar/HelloWorld.jar
```

## Varargs

An arbritary number of values can be passed to a method witih a construct called *varargs*, introduced with Java 1.5.

* [Varargs](https://docs.oracle.com/javase/1.5.0/docs/guide/language/varargs.html)
* [Oracle JavaOO Tutorial](https://docs.oracle.com/javase/tutorial/java/javaOO/arguments.html)

While it would be possible to just have an array as a parameter and set that up before calling the method, this simplifies the process. To use varargs, the type of the last parameter is followed by an ellipsis, a space, and  the parameter name. The method can be called with any number of that parameter, including none.