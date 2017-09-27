# Docker for Java Developers

* Lynda.com course on using Java with Docker.
* [Java in a World of Containers](https://www.youtube.com/watch?v=t0HkM7g5bxA)

## Create a Java Docker Image

OpenJDK Image:

```Dockerfile
# Pull openjdk container with Java SE 9 and then echo the java version
FROM openjdk:9

CMD java -version
```

Other image tag options:

* `openjdk:jdk-alpine` - get the latest JDK on Alpine Linux

Oracle Java SE Image:

Prerequisites:

* Sign in to store.docker.com and fill in form for Oracle Java SE
* Login into Docker locally via the CLI, `docker login` and enter username and password when prompted

```Dockerfile
FROM store/oracle/serverjre:8

CMD java -version
```

IBM Java Image:

```Dockerfile
FROM ibmjava

CMD java -version
```

## Examples

Setting up a webapp on Wildfly:

Here the default command is not overwritten, so that the war is then deployed and the wildfly server started and accessible via the relevant url (probably localhost:8080).

```Dockerfile
FROM jboss/wildfly

COPY webapp.war /opt/jboss/wildfly/standalone/deployments/webapp.war
```

Packaging and running a jar:

```Dockerfile
FROM openjdk:jdk-alpine

COPY myapp/target/myapp-1.0-SNAPSHOT.jar /deployments/

CMD java -jar /deployments/myapp-1.0-SNAPSHOT.jar
```

## Docker and Maven

Maven plugins for working with Docker. There are several plugins, but a well documented and maintained plugin is from fabric8, [docker-maven-plugin](https://github.com/fabric8io/docker-maven-plugin). With documentation [here](https://dmp.fabric8.io/).

* `mvn package -Pdocker`
* `mvn install -Pdocker`

## Docker and Gradle

Gradle plugins for working with Docker. There are also several plugins for working with Docker for Gradle.
Benjamin Muschko's Gradle plugin is currently the most popular, available on GitHub [here](https://github.com/bmuschko/gradle-docker-plugin).

* `./gradlew dockerBuildImage`
* `./gradlew startContainer`

Doesn't currently work for me, seems related to these issues: [issue 1](https://github.com/bmuschko/gradle-docker-plugin/issues/366) and [issue 2](https://github.com/bmuschko/gradle-docker-plugin/issues/411)