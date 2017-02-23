# POM Reference - Project Object Model
-------
## Intro
Notes from [Maven's POM Reference page](https://maven.apache.org).

The pom.xml project file is an XML representation of a Maven Project. It covers the who, what, where, as well as the when & how. It is declarative, unlike Ant which is procedural.

# The Basics
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
Dependencies, Transitive Dependencies, Inheritance, Aggregation

### Dependencies
The POM lists the dependencies, these dependencies can in turn resolve their own dependencies (transitive dependencies). A dependency is specified via its coordinates, with additional options.

Classifier: an optional & arbitrary string that -if present- is appended to the artifact name just after the version number (the generated artifact??). Helps to distinguish artifacts built from the same POM but which have different content, e.g. a project with an artifact targeting JDK1.6 but at the same time also an artifact targeting JDK1.7.

Type: corresponds to an artifact's packaging type. Refer back to Maven POM Ref.

Scope: There are 5 scopes, refers to the classpath of the task at hand (compiling, runtime, etc), & scope is also how to limit transitive dependencies.
* compile - default scope
* provided - ?
* runtime - indicates the dependency is not required for compilation, but is required for execution
* test - not required for normal use of application, and is only available for test & execution phases
* system - similar to provided (?) except that you have to provide the jar which contains it explicitly, the artifact is always available and not looked up in a repository.

systemPath: this requires an absolute path and should only be used if the scope is system.

optional: used when a projects (Project A) own dependency isn't necessary if another project (Project B) is using that project (Project A). See Maven's POM Ref.

Non-Maven dependcies rquire workarounds to use in a maven project. Maven really wants you to only use dependcies which are also Maven Projects. If that's just not possible, then there are 3 workarounds:

1. Install the dependency locally:
`mvn install:install-file -Dfile=non-maven-proj.jar -DgroupId=com.some.groupId -DartifactId=non-maven-proj -Dversion=1 -Dpackaging=jar`

2. Create a repo and deploy there, deploy:deploy-file, this is basically the same as option 1, but better if a team is working on the project.

3. Set the dependency scope to system and define systemPath. This is not recommended.

#### Dependency Versions
Dependencies' version element defines version requirements using the following syntax:

* 1.0 : a soft requirement, more of a recommendation and can match other versions if the given version isn't available.
* [1.0] : a hard requirement, it must be [this] version.
* (,1.0] : x <= 1.0, the version musts be less than or equal to the version given
* [1.2,1.3] : 1.2 <= x <= 1.3, the version must be equal to or between the two specified versions
* [1.0,2.0) : 1.0 <= x < 2.0, the version must be greater than or equal to 1.0, and less than 2.0
* [1.5,) : x >= 1.5, x must be greater than or equal to the version
* (,1.0],[1,2,) : x <= 1.0 or x >= 1.2; multiple sets are comma-separated. Here the version has to be 1.0 or less, or 1.2 and greater, so 1.1 cannot be used. Does this apply to minor versions as well, e.g. would 1.0.1 not be usable.

#### Exclusions

### Inheritance

#### The Super POM

### Aggregation (or Multi-Module)
A project with modules is known as a multimodule, or aggregator project. Modules are projects that this POM lists, and are executed as a group. A POM packaged project may aggregate the build of a set of projects by listing them as modules which are relative directories to those projects.
## Properties
Maven properties are value placeholders, like properties in Ant.
Their values are accessible within a POM using the notation ${X}.
These properties are essentially variables, or are they constants, can they be changed at different stages of the POM?

There are 5 different styles:
1. env.X : prefixing a variable with 'env.' will return the shell's environment variable. E.g. ${env.PATH} contains the PATH environment variable.
2. project.x : a dot notated path in the POM will contain the corresponding element's value. E.g. `<project><version>1.0</version></project>` is accessible via `${project.version}`
3. settings.x : a dot notated path in the settings.xml will contain the corresponding elements's value, works the same as project.x
4. Java System Properties: All properties accessible via java.lang.System.getProperties() are available as POM properties, such as ${java.home}.
5. x : Set within a <properties /> element in the POM. The value of `<properties><someVar></someVar></properties>` may be used as ${someVar}.

# Build Settings
Beyond the already covered POM basics, there are two additional elements important to basic competency with the POM. These are the build element and the reporting element

## Build
From Maven's POM Reference, verbatim: According to the POM 4.0.0 XSD (XML Schema Definition) the build element is conceptually divided into two parts: there is a BaseBuild type which contains the set of elements common to both build elements (the top-level build element under project and the build element under profiles, covered below); and there is the Build type, which contains the BaseBuild set as well as more elements for the top level definition.

//Rewrite once this is better understood

To break it down, the same xml element build is used for both, but has different corresponding elements based on the context/placement in the POM, but also shares a set of base elements, right? The two contexts are the 'project build' as a direct child of project, the root node, & the 'profile build' which is nested in the profile element.

### The BaseBuild Element Set
```
<build>
  <defaultGoal>install</defaultGoal>
  <directory>${basedir}/target</directory>
  <finalName>${artifactId}-${version}</finalName>
  <filters>
    <filter>filters/filter1.properties</filter>
  </filters>
  ...
</build>
```

* defaultGoal :
* directory : build target directory
* finalName :
* filter :

#### Resources


### The Build Element Set
#### Directories

#### Extensions

## Reporting

# More Project Information

# Environment Settings


# Buffer
