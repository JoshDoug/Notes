# The Platform Environment


## Configuration Utilities
Covers some of the config utils that help an application access its startup context.

### Properties
Properties are configuration values managed as key-value pairs, both the key and value are String values. The key is used to retrieve the value, like a variable. E.g. an application capable of downloading files might use a property named download.lastDirectory to keep track of the directory used for the last download.

To manage properties, create instances of [java.util.Properties](https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html)

Properties file just #comments and key-value pairs:

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

## System Utilities


## PATH & CLASSPATH
