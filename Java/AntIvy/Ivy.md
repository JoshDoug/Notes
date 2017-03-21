# Using Apache Ivy
Using Apache Ivy, with Ant.
According to the Apache Ivy website, Ivy is a tool for managing (recording, tracking, resolving, and reporting) project dependencies.

Install ivy when installing ant, with brew:
`brew install ant --with-ivy`

## Basic Example ivy.xml and build.xml

ivy.xml
```
<ivy-module version="2.0">
  <info organisation="com.joshuastringfellow" module="HelloWorld">
  <dependencies>
    <dependency org="org.apache.commons" name="commons-lang3" rev="3.5" />
    <dependency org="commons-cli" name="commons-cli" rev="1.4" />
  </dependencies>
</ivy-module>
```

build.xml
```
<project xmlns:ivy="antlib:org.apache.ivy.ant" name="HelloWorld" default="run">

  - - -

  <target name="resolve" description="Retrieve dependencies with Ivy">
    <ivy:retrieve />
  </target>
</project>
```

Some maven projects that are actually a bundle do not resolve successfully if you just set the dependency to org, name, & rev. Instead you might have to add bundle as a type to the ivy:retrieve task or check the documentation for that dependency to see if they specify how it should be done, e.g. log4j: https://logging.apache.org/log4j/2.x/maven-artifacts.html

### Ivy-Module
https://ant.apache.org/ivy/history/trunk/ivyfile.html
Ivy-module is currently version 2.0, not sure how it's versioned but the link above covers the version under 'attributes' at the bottom of the page.


## Self hosted Ivy
This involves setting Ivy as a dependency of the project itself, this way only Ant needs to be installed on the system.

If Ivy is already installed on the system then that takes precedence over the self hosted Ivy, which makes the following info somewhat worthless.

This example build.xml sets up a self hosted ivy, probably a good idea to change the version to 2.4.0 or w/e the current stable version is, also according to it's own descriptin it is not a good example of best practice:
https://ant.apache.org/ivy/history/latest-milestone/samples/build.xml
