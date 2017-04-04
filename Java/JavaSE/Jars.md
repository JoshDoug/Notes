# Packaging Programs in JAR Files
The Java Archive (JAR) file format allows bundling of multiple class files and auxilliary resources into a single archive file.

Benefits of the JAR file format:
* Security - Digitally sign JARs
* Compression - JAR format can compress files
* Packaging for extensions - The extensions framework provides a means by which you can add functionality to the Java core platform, and the JAR file format defines the packaging for extensions. By using the JAR file format, you can turn your software into extensions as well.
* Package Sealing - Packages stored in JAR files can be optionally sealed so that the package can enforce version consistency. Sealing a package within a JAR file means that all classes defined in that package must be found in the same JAR file.
* Package Versioning - A JAR file can hold data about the files it contains, such as vendor and version information.
* Portability - The mechanism for handling JAR files is a standard part of the Java platform's core API.

# Using JAR Files: The Basics
JAR files are packaged with the ZIP file format, so they can be used for lossless data compression, archiving, decompression, and archive unpacking.

JARs are created using the Java Archive Tool, aka the jar tool, using the `jar` command.

Common JAR file operations:

| Operation | Command |
|-----------|---------|
|To create a JAR file|jar cf jar-file input-file(s)|
|To view the contents of a JAR file|jar tf jar-file|
|To extract the contents of a JAR file|jar xf jar-file|
|To extract specific files from a JAR file|jar xf jar-file archived-file(s)|
|To run an application packaged as a JAR file (requires the Main-class manifest header)|java -jar app.jar|
|To invoke an applet packaged as a JAR file|`<applet code=AppletClassName.class archive="JarFileName.jar" width=width height=height></applet>`|

## Creating a JAR File

## Viewing the Contents of a JAR File

## Extracting the Contents of a JAR File

## Updating a JAR File

## Running JAR-Packaged Software

# Working with Manifest Files: The Basics

# Signing and Verifying JAR Files

# Using JAR-related APIs
