# Docker for Java Developers

Lynda.com course on using Java with Docker.

## Create a Java Docker Image

OpenJDK Image:

```Dockerfile
# Pull openjdk container with Java SE 9 and then echo the java version
FROM openjdk:9

CMD java -version
```

Oracle Java SE Image:

Prerequisites:

* Sign in to store.docker.com and fill in form for Oracle Java SE
* Login into Docker locally via the CLI, `docker login` and enter username and password when prompted

```Dockerfile
FROM store/oracle/serverjre:8

CMD java -version
```