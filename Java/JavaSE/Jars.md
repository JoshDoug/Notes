# Packaging Programs in JAR Files

The Java Archive (JAR) file format allows bundling of multiple class files and auxilliary resources into a single archive file.

Benefits of the JAR file format:

* Security - Digitally sign JARs
* Compression - JAR format can compress files
* Packaging for extensions - The extensions framework provides a means by which you can add functionality to the Java core platform, and the JAR file format defines the packaging for extensions. By using the JAR file format, you can turn your software into extensions as well.
* Package Sealing - Packages stored in JAR files can be optionally sealed so that the package can enforce version consistency. Sealing a package within a JAR file means that all classes defined in that package must be found in the same JAR file.
* Package Versioning - A JAR file can hold data about the files it contains, such as vendor and version information.
* Portability - The mechanism for handling JAR files is a standard part of the Java platform's core API.

## Using JAR Files: The Basics

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

### Creating a JAR File

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

```dir
Project/
├── Main.java
├── audio/
├── images/
```

Where audio and images are folders containing assets used by Main, then to package this into a jar you would run: `jar cvf Project.jar Main.java audio images`, or as long as there are no unwanted files in the project, you could run: `jar cvf Project.jar *`. Both these examples retain their relative path names and directory structure within the JAR.

To create a JAR from the project where all the files are in the parent directory, run: `jar cf ImageAudio.jar -C images . -C audio .`, with the full stop. The -C images part of this command directs the Jar tool to go to the images directory, and the . following -C images directs the Jar tool to archive all the contents of that directory. The -C audio . part of the command then does the same with the audio directory

### [Viewing the Contents of a JAR File](https://docs.oracle.com/javase/tutorial/deployment/jar/view.html)

Basic command to view JAR contents: `jar tf jar-file`

* The t option specifies a table of contents
* The f options specifies the JAR file
* You can also add the v option, for verbose, which provides additional info such as file sizes and dates modified

The order of t and f doesn't matter, but there must not be any space in between them.

### [Extracting the Contents of a JAR File](https://docs.oracle.com/javase/tutorial/deployment/jar/unpack.html)

Basic command to extract JAR contents: `jar xf jar-file`
To speciffy specific files to extract: `jar xf jar-file archived-files(s)` specify multiple files with a space seperated list

* x option is to extract
* f option is to specify the jar file

When extracting a JARs contents, the contents are copied out and the original JAR remains unchanged. The extracted files and directories reflect the relevant file paths and directories within the JAR. This also means that to extract a file in a directory, you also have to specify the directory it is in within the jar. E.g. to extract the manifest: `jar xf example.jar META-INF/MANIFEST.MF`.

Caution: When it extracts files, the Jar tool will overwrite any existing files having the same pathname as the extracted files.

### [Updating a JAR File](https://docs.oracle.com/javase/tutorial/deployment/jar/update.html)

The Jar tool provides a `u` option which you can use to update the contents of an existing JAR file by modifying its manifest or by adding files.
The basic command to do this: `jar uf jar-file input-file(s)`

Any files already in the archive having the same pathname as a file being added will be overwritten.

So if you wanted to add a new image to the images directory in a jar you've already made, you could run: `jar uf TicTacToe.jar images/new.gif` instead of needing to recreate the jar. If you're unsure of what files and directory structure the jar has, then you can just view the contents first.

### [Running JAR-Packaged Software](https://docs.oracle.com/javase/tutorial/deployment/jar/run.html)

Link also covers applets packaged in JAR files, but who cares about applets.

The basic command to run a jar: `java -jar jar-file`

The -jar flag tells the launcher that the app is packaged in the JAR format. You can only specify one JAR file, whcih must contain all of the application-specific code. To run this command the jar must have a specified entry point, either in the JAR's manifest, or in the command itself.
In the manifest the entry point is specified like so: `Main-Class: classname`.

To run a jar without a manifest specified entry point, run: `jar -cp dir/jar-file com.package.MainClassName` where MainClassName refers to the entry point/Main class. This also shows how you can run a jar from another directory, just pass the path to it, relevant or absolute.

## Working with Manifest Files: The Basics

The manifest is a special file that can contain information about the files packaged in a JAR file. By tailoring this "meta" information that the manifest contains, you enable the JAR file to serve a variety of purposes.

### [Understanding the Default Manifest](https://docs.oracle.com/javase/tutorial/deployment/jar/defman.html)

When a JAR is created, it automatically gets a default manifest file, an archive can only have one manifest, and it always has the relative path `META-INF/MANIFEST.MF`

The default manifest simply contains:

```manifest
Manifest-Version: 1.0
Created-By: 1.7.0_06 (Oracle Corporation)
```

These lines illustrates how manifest entries are set, using "header: value" pairs.

### [Modifying a Manifest File](https://docs.oracle.com/javase/tutorial/deployment/jar/modman.html)

Creating a jar with a modified manifest, the basic command has this format: `jar cfm jar-file manifest-addition input-file(s)`

The `manifest addition` if a file with additions to the default manifest file that gets added, not a replacement per se, at least as far as I understand it. The m option in the manifest *seems* to refer to merging options rather than standing for manifest. So you are merging options from your own manifest, not specifying the manifest. In practice this might be irrelevant. The name of the manifest is also irrelevant, as is the file extension, myManifest, myManifest.txt, and myManifest.md will all work as long as the contents are plaintext.

Regarding the example, the m and f options must be in the same order as the corresponding arguments.

Warning: The text file must end with a new line or carriage return. The last line will not be parsed properly if it does not end with a new line or carriage return.

### [Setting an Application's Entry Point](https://docs.oracle.com/javase/tutorial/deployment/jar/appman.html)

To specify a the entry point for a JAR use the `Main-Class` header in the manifest: `Main-Class: classname`.
The entry point it just a class that has a main method.

Use the `e` flag to create or override the manifest's Main-Class attribute, this can be used while creating or updating a JAR.

To set the class to AnotherMain.class: `jar cfe app.jar MyApp MyApp.class`, then you can run the jar as normal: `java -jar app.jar`.

When specifying the entry point class it can either be done the package way `com.package.Main` or relative directory `com/package/Main.class`, not sure if .class is absolutely necessary.

### [Adding Classes to the JAR File's Classpath](https://docs.oracle.com/javase/tutorial/deployment/jar/downman.html)

Sometimes you need to reference classes in other JAR files from within a JAR file, as dependencies.

To do this you specify classes to include in the Class-Path header field in the manifest file of an application. The Class-Path header takes the following form: `Class-Path: jar1-name jar2-name directory-name/jar3-name`

By using the Class-Path header in the manifest, you can avoid having to specify a long -classpath or -cp flag when invoking Java to run the application.

#### Example

You have an application jar, app.jar, that is dependent on another jar, say util.jar. They are in the same directory.
To set the classpath for app.jar to include util.jar, follow the steps:

Create a text file, e.g. manifest.txt, that contains `Class-Path: util.jar`, no path needed since they are in the same dir.
Then create the app.jar by running: `jar cfm app.jar manifest.txt build/classes/*.class`.

Now when app.jar is run it can load the classes from util.jar.

### [Setting Package Version Information](https://docs.oracle.com/javase/tutorial/deployment/jar/packageman.html)

If you need to, you can include package version information in a manifest:

|Header|Definition|
|------|----------|
|Name|The name of the specification|
|Specification-Title|The title of the specification|
|Specification-Version|The version of the specification|
|Specification-Vendor|The vendor of the specification|
|Implementation-Title|The title of the implementation|
|Implementation-Version|The build number of the implementation|
|Implementation-Vendor|The vendor of the implementation|

The definitions seem a little redundant.

One set of these headers can be assigned to each package. The versioning headers should appear directly beneath the `Name` header for the package:

```config
Name: java/util/
Specification-Title: Java Utility Classes
Specification-Version: 1.2
Specification-Vendor: Example Tech, Inc.
Implementation-Title: java.util
Implementation-Version: build57
Implementation-Vendor: Example Tech, Inc.
```

More info on package version headers: [Package Versioning Specification](https://docs.oracle.com/javase/8/docs/technotes/guides/versioning/spec/versioning2.html#wp89936)

### [Sealing Packages within a JAR](https://docs.oracle.com/javase/tutorial/deployment/jar/sealman.html)

Packages within JAR files can be optionally sealed, which means that all classes defined in that package must be archived in the same JAR file. You might want to seal a package, for example, to ensure version consistency among the classes in your software.

Does this mean you cannot optionally update a jar with new versions of classes within that jar that are part of packages which have been sealed?

A package is sealed by setting the header in the manifest under the package name:

```config
Name: com/companyName/packageName
Sealed: true
```

Still not clear on this.
TODO: Re-read and research.

### [Enhancing Security with Manifest Attributes](https://docs.oracle.com/javase/tutorial/deployment/jar/secman.html)

These attributes only seem to be relevant to Java Applets and Java Web Start applications, so not of interest but link is available.

## Signing and Verifying JAR Files

Allows users to verify the signatures of JARs, and the JARs can be granted additional software security priveleges they wouldn't normally get (is that only for Applets/RIAs).

### [Understanding Signing and Verification](https://docs.oracle.com/javase/tutorial/deployment/jar/intro.html)

Probably never gonna use this, so check the link.

[X.509 Cets](https://docs.oracle.com/javase/8/docs/technotes/guides/security/cert3.html)

### [Signing JAR Files](https://docs.oracle.com/javase/tutorial/deployment/jar/signing.html)

Basic command for signing a jar: `jarsigner jar-file alias` where alias is typically the name of the key owner and can be used to identify a key in a keystore.

* `alias` is the alias identifying the private key that's to be used to sign the JAR file, and the key's associated certificate.

The jarsigner tool prompts for a password for the keystore and alias.

#### How does one create a keystore, eh? Hmm

Would be good to know, eh.

### [Verifying Signed JAR Files](https://docs.oracle.com/javase/tutorial/deployment/jar/verify.html)

Often the Java Runtime Environment can verify signed applets & jars, but you can also do this yourself, ya nerds.
Useful for testing your own signed jars have been signed properly.

Basic command: `jarsigner -verify jar-file` easy. This just tests that the signature included with the jar matches the jar.

## Using JAR-related APIs

Some of the APIs:

* The [`java.util.jar`](https://docs.oracle.com/javase/8/docs/api/java/util/jar/package-summary.html) package
* The [`java.net.JarURLConnection`](https://docs.oracle.com/javase/8/docs/api/java/net/JarURLConnection.html) class
* The [`java.net.URLClassLoader`](https://docs.oracle.com/javase/8/docs/api/java/net/URLClassLoader.html) class

The example used for this by Oracle also contains some reflection stuff.

### [The JarClassLoader Class](https://docs.oracle.com/javase/tutorial/deployment/jar/jarclassloader.html)

The [JarClassLoader Class](https://docs.oracle.com/javase/tutorial/deployment/jar/examples/JarClassLoader.java)

### [The JarRunner Class](https://docs.oracle.com/javase/tutorial/deployment/jar/jarrunner.html)

The [JarRunner Class](https://docs.oracle.com/javase/tutorial/deployment/jar/examples/JarRunner.java)
