# Docker Compose

Most applications have multiple components, e.g. a webserver, database, application server, etc. So if an application is made up of multilple components it ideally would be modularised, each component run as a container, and this is where Docker Compose comes in. Docker Compose makes it easy to run multicontainer applications.

Configuration is defined in one or more files, docker-compose.yml by default. A docker-compose.override.yml can also exist which overrides certain parts of the docker-compose.yml and is merged into a single Docker Compose definiton.

A single command is used to manage all services at once, to bring them up, build all the images, shut them all down.

* Docker Compose version: `docker-compose -v`
* Docker Compose help: `docker-compose` adding `help` and `--help` are optional and thus redundant
* Help about a specific command: `docker-compose up --help` - get help on the `up` command
* Check logs: `docker-compose logs`, follow log with `docker-compose logs -f`
* Check services: `docker-compose ps`
* Start service with compose: `docker-compose up -d`
* Stop service with compose: `docker-compose down`, this will stop the containers and remove them

## Docker Compose Options

* Multiple projects using `-p` - create multiple isolated environments on a host
* Default override `docker-compose.override.yml` - replaces or extends values
  * Single value options like image replace the older value
  * Multivalue options like ports are concatendated; newer values and higher precedence

## Docker Compose Configuration Files

Simple sample docker-compose.yml:

```yml
version: '3'
services:
  web:
    image: jboss/wildfly
    volumes:
      - ~/Learning/Java/docker-for-java/chapter3/deployment:/opt/jboss/wildfly/standalone/deployments
    ports:
      - 8080:8080
```

Multicontainer application with docker-compose:

A sample application with a Wildfly web server that talks to the Couchbase NoSQL document database using the N1QL (SQL with JSON) Couchbase programming language.

```yml
version: '3'
services:
  web:
    image: arungupta/couchbase-javaee:travel
    environment:
      - COUCHBASE_URI=db
    ports:
      - 8080:8080
      - 9990:9990
    depends_on:
      - db
  db:
    image: arungupta/couchbase:travel
    ports:
      - 8091:8091
      - 8092:8092
      - 8093:8093
      - 11210:11210
```

The COUCHBASE_URI=db environment variable set in the compose config is a system ennvironment variable and can be accessed however the langauge being used by an application would normally access a system env, e.g. in Java it can be accessed like so: `String result = System.getenv("COUCHBASE_URI)` which will return `"db"`. A possible alternative is also `String result = System.getProperty("COUCHBASE_URI")` if the variable is set as a Java property.

