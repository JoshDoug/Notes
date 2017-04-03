# The Platform Environment


## Configuration Utilities
Covers some of the config utils that help an application access its startup context.

### Properties
Properties are configuration values managed as key-value pairs, both the key and value are String values. The key is used to retrieve the value, like a variable. E.g. an application capable of downloading files might use a property named download.lastDirectory to keep track of the directory used for the last download.

To manage properties, create instances of [java.util.Properties](https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html)

Properties file just #comments and key-value pairs, like an .ini key/property:

```
#Mon Apr 03 19:47:12 BST 2017
dbpassword=demoPassword
database=localhost
dbuser=demoUser
```

Can be loaded from and to XML using `loadFromXML(InputStream)` and `storeToXML(OutputStream, String, String)`, uses UTF-8 by default.

XML equivalent of above example, created using storeToXML:

```
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<!DOCTYPE properties SYSTEM "http://java.sun.com/dtd/properties.dtd">
<properties>
<comment>Output to XML</comment>
<entry key="dbpassword">password</entry>
<entry key="database">localhost</entry>
<entry key="dbuser">mkyong</entry>
</properties>
```

See the java.util.Properites documentation and [Java Properties Tutorial](https://docs.oracle.com/javase/tutorial/essential/environment/properties.html) for examples on how to programmatically manipulate and manage properties.

### Command-Line Arguments
Running a basic java program, `java program arg1 arg2 arg3`

E.g. `java Echo Drink Hot Java Coffee`

With the program echo:

```
public class Echo {
    public static void main (String[] args) {
        for (String s: args) {
            System.out.println(s);
        }
    }
}
```

Would take in Drink, Hot, Java, Coffee as separate arguments in the string args array. With the output:

```
Drink
Hot
Java  
Coffee
```

If you wanted to pass an argument that contained a space, you'd need to put it in quotes: `java Echo Drink Hot "Java Coffee"`, this would have the output:

```
Drink
Hot
Java Coffee
```

Note, all arguments are passed as strings, so if your program is expecting numbers, you'll need to parse them:

```
int firstArg;
if (args.length > 0) {
    try {
        firstArg = Integer.parseInt(args[0]);
    } catch (NumberFormatException e) {
        System.err.println("Argument" + args[0] + " must be an integer.");
        System.exit(1);
    }
}
```

### Environment Variables
You can retrieve normal system environment variables in Java. Setting the environment variables depends on the system, e.g. `export $EXAMPLE="an example"` on UNIX-like systems.

Example of getting all the environment variables using `System.getenv()`:

```
import java.util.Map;

public class EnvMap {
    public static void main (String[] args) {
        Map<String, String> env = System.getenv();
        for (String envName : env.keySet()) {
            System.out.format("%s=%s%n",
                              envName,
                              env.get(envName));
        }
    }
}
```

Example of getting a specific environment variables:

```
public class Env {
    public static void main (String[] args) {
        for (String env: args) {
            String value = System.getenv(env);
            if (value != null) {
                System.out.format("%s=%s%n",
                                  env, value);
            } else {
                System.out.format("%s is"
                    + " not assigned.%n", env);
            }
        }
    }
}
```

When accessing System Properties it's best to access them using the java provided way of accessing them, instead of via environment variables to avoid inconsistencies between operating systems.

#### Passing Environment Variables to New Processes
When a Java application uses a ProcessBuilder object to create a new process, the default set of environment variables passed to the new process is the same set provided to the application's virtual machine process. The application can change this set using ProcessBuilder.environment.

### Other Configuration Utilities
* [Preferences API](https://docs.oracle.com/javase/8/docs/technotes/guides/preferences/index.html)
* JAR Manifest - more info [here](https://docs.oracle.com/javase/tutorial/deployment/jar/index.html)
* Java Web Start uses a JNLP file - [JWS Tutorial](https://docs.oracle.com/javase/tutorial/deployment/webstart/index.html)
* Services - [Service Loader](https://docs.oracle.com/javase/8/docs/api/java/util/ServiceLoader.html) & [Extensions](https://docs.oracle.com/javase/tutorial/ext/index.html)

## System Utilities


## PATH & CLASSPATH
