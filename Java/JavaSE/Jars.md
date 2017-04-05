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
Basic JAR creation command: `jar cf <jar-file> <input-file(s)>`
* `c` - for create
* `f` - indicates output should go to a file instead of stdout
* `jar-file` - name of the jar file, has a .jar extension by convention, though this is not required.
* `input-file` - this is the input file or files, with multiple files it is a space seperated list. The * wildcard can also be used. If any of the `input-file`s are directories, the contents of the directories will be added to the JAR recursively.

The `c` and `f` options can appear in either order, but cannot have any space between them.
This command will generate a compressed JAR and place it in the current directory, it will also generate a default manifest file for the JAR.

Additional options:

|Option|Description|
|------|-----------|
|v|Produces verbose output on stdout while the JAR is being built. The output tells you the name of each file as it's added to the JAR file|
|0|Zero indicates that the JAR shouldn't be compressed, uncompressed jars can sometimes load faster|
|M|Indicates that the default manifest file should not be produced|
|m|Used to include manifest information from an existing manifest file, `jar cmf manifest-file jar-file input-file(s)`|
|-C|To change directories during execution of the command|

If a project had the following directory structure:
```
Project/
├── Main.java
├── audio/
├── images/
```
Where audio and images are folders containing assets used by Main, then to package this into a jar you would run: `jar cvf Project.jar Main.java audio images`, or as long as there are no unwanted files in the project, you could run: `jar cvf Project.jar *`. Both these examples retain their relative path names and directory structure within the JAR.

To create a JAR from the project where all the files are in the parent directory, run: `jar cf ImageAudio.jar -C images . -C audio .`, with the full stop. The -C images part of this command directs the Jar tool to go to the images directory, and the . following -C images directs the Jar tool to archive all the contents of that directory. The -C audio . part of the command then does the same with the audio directory

## Viewing the Contents of a JAR File

## Extracting the Contents of a JAR File

## Updating a JAR File

## Running JAR-Packaged Software

# Working with Manifest Files: The Basics

## [Understanding the Default Manifest](https://docs.oracle.com/javase/tutorial/deployment/jar/defman.html)
When a JAR is created, it automatically gets a default manifest file, an archive can only have one manifest, and it always has the relative path `META-INF/MANIFEST.MF`

The default manifest simply contains:
```
Manifest-Version: 1.0
Created-By: 1.7.0_06 (Oracle Corporation)
```

These lines illustrates how manifest entries are set, using "header: value" pairs.

## Modifying a Manifest File

# Signing and Verifying JAR Files

# Using JAR-related APIs
