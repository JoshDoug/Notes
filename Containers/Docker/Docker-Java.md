# Docker for Java Developers

Lynda.com course on using Java with Docker.

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

```Dockerfile
FROM jboss/wildfly

COPY webapp.war /opt/jboss/wildfly/standalone/deployments/webapp.war
```