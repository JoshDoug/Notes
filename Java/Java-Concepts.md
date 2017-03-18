# OO Patterns, General Java Concepts etc
Might extend to cover JVM, JRE, JDK usage and options.


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

# Running from the CLI
Setting up and running a project from the command line (HelloWorld)
(Using the pre-Ant part of Ant's tutorial)

Create the project directory and files within it:

```
mkdir -pv HelloWorld/{build/{classes,jar},src/oata}
cd HelloWorld
```
Then create the HelloWorld java source file:
```
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
```
javac -sourcepath src -d build/classes src/oata/HelloWorld.java
java -cp build/classes oata.HelloWorld
```

Then create the manifest file:
```
echo "Main-Class: oata.HelloWorld" > myManifest
```

Then create and run a jar of it:
```
jar cfm build/jar/HelloWorld.jar myManifest -C build/classes .
java -jar build/jar/HelloWorld.jar
```

For more argument options see:
* man java
* man javac
* man jar
* man javah - C header and stub file generator
* man jps
* man jstack
* man orbd
* man schemagen
* man wsimport
* man extcheck
* man javadoc
* man jconsole
* man jmap
* man jstat
* man pack200
* man serialver
* man xjc
* man idlj
* man jdb
* man jstatd
* man policytool
* man servertool
* man rmic
* man tnameserv
* man jarsigner
* man javap
* man jhat
* man jrunscript
* man keytool
* man rmid
* man unpack200
* man jinfo
* man jsadebugd
* man native2ascii
* man rmiregistry
* man wsgen

Etc?

Google for:
* jcmd
* jdeps
* jjs
* jvisualvm
* javapackager
* javafxpackager
* jmc
