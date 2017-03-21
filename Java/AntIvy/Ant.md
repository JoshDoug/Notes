# Apache Ant
Ant is a built tool, typically used with Ivy - a dependency management(? or fetching) tool.

Ant uses build files written in XML.

Installing Ant (with ivy): `brew install ant --with-ivy`.
It's allso possible to just copy the ivy jar into the ant lib or libexec/lib directory, if you're using windows for example.

## Build Files
A buildfile contains on project and at least one (default target.
Targets contains task elements (?). Each task element of the buildfile can have an ```id``` attribute with which it can latter be referred to by. An id has to be unique (duh).

A project has three attributes:
* name - the name of the project (not required)
* default - default target to use when no target is supplied (not required, but every project has an implicit target which will be run instead?)
* basedir - used for the base directory from which any class calculations will be done, by default it is the parent directory of the build.xml (not reuired - will default to directory of build.xml)

### Targets and Tasks
Each project defines one or more *targets*, and each target is a set of *tasks* that need to be executed. A target is a specific element, a task is not. A task is a piece of code that can be executed that has a specific structure:
`<taskname id="taskID" attribute1="value1" attribute2="value2" etc... />`

A task has a name, an optional id, and attributes with values. Overall a task is an object, which can be referred to in other tasks or scripts. There might be backward compatibility issues with this sort of behavior?? Who knows. Apparently *task instances* will be know more and will be replaced by *proxies* or w/e.

Built in tasks: https://ant.apache.org/manual/tasklist.html

Write your own: https://ant.apache.org/manual/develop.html#writingowntask

### Properties
A property is essentially a constant/variable that can be referrenced later on in the build file, concatenated, etc.

`<property name="src" location="src" value="src" />`

Location or value? Tutorial uses value, Manual uses location....

They can also be set outside of ant - how? Normal system environment variables??

More on ant  properties: https://ant.apache.org/manual/properties.html

### Putting it together to make a basic build.xml project file

```
<project name="HelloWorld" basedir="." default="main">
  <description>
  This buildfile is used to build the HelloWorld project, this description is useful but not required. No parameters, online desc: https://ant.apache.org/manual/Types/description.html
  </description>
  <!-- XML Comment, set global properties for this build -->
  <property name="src" location="src" />

</project>
```

### Path-like Structures
This is what we're looking for - how to set up the classpath to include our log4j.xml configuration file, right? It needs to be in the classpath...but does that require it to be in the $CLASSPATH or will the ant classpath do?

You can use `:` or `;` as classpath seperators and Ant will determine which is appropriate for the current operating system. Nice.

#### Resources (used by paths i guess..)

#### FileSet

#### DirSet
