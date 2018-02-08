# POM Tips

## Set Java version

* [Specify compiler version for Maven to use with the maven-compiler-plugin](https://maven.apache.org/plugins/maven-compiler-plugin/)

## Set mainClass

This allows a jar to be run with a double click, this would otherwise fail as java would fail to find the main class.

* [maven-jar-plugin](https://maven.apache.org/plugins/maven-jar-plugin/)
* [maven-archiver](https://maven.apache.org/shared/maven-archiver/index.html)
* [Stackoverflow - adding mainclass in POM with folderpath](https://stackoverflow.com/questions/29920434/maven-adding-mainclass-in-pom-xml-with-the-right-folderpath)

## Packaging Maven Dependencies

* [Stackoverflow question about executable jar](https://stackoverflow.com/questions/15990258/maven-cant-execute-jar)
* [Maven Shade plugin for packaging dependencies into an 'Uber' jar](https://maven.apache.org/plugins/maven-shade-plugin/)