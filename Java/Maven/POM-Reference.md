# POM Reference - Project Object Model
Notes from [Maven's POM Reference page](https://maven.apache.org).

The pom.xml project file is an XML representation of a Maven Project. It covers the who, what, where, as well as the when & how. It is declarative, unlike Ant which is procedural.

## Maven Coordinates - groupId:artifactId:version
e.g. `org.apache.maven.plugins:maven-deploy-plugin:2.7`

* Who: groupdId - doesn't need to be dot notation or conform to package notation, but probably should.
* What: artifactId ~ normally the project name but can be different, e.g maven's deploy plugin is maven-deploy-plugin instead of just 'deploy'
* When - the version

Packaging is an optional part of the coordinates along with classifier.

Packaging defaults to jar if left undeclared, other options (goals):
* jar (Java Archive)
* war (Web Archive)
* ear (Enterprise Application aRchive)
* rar (Roshal Archive)
* ejb (Enterprise Java Bean)
* par (Parity Archive)
* pom (Project Object Model)
* maven-plugin

Classifier - unlikely to use, check Maven's POM Reference.

e.g. `groupdId:artifactId:packaging:classifier:version`

## POM Relationships
### Dependencies, Transitive Dependencies, Inheritance, Aggregation
The POM lists the dependencies, these dependencies can in turn resolve their own dependencies (transitive dependencies). A dependency is specified via its coordinates, with additional options.

Classifier: an optional & arbitrary string that -if present- is appended to the artifact name just after the version number (the generated artifact??). Helps to distinguish artifacts built from the same POM but which have different content, e.g. a project with an artifact targeting JDK1.6 but at the same time also an artifact targeting JDK1.7.

Type: corresponds to an artifact's packaging type. Refer back to Maven POM Ref.

Scope: There are 5 scopes, refers to the classpath of the task at hand (compiling, runtime, etc), & scope is also how to limit transitive dependencies.
* compile
* provided
* runtime
* test
* system









# Buffer
