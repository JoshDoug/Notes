# Docker Compose

Most applications have multiple components, e.g. a webserver, database, application server, etc. So if an application is made up of multilple components it ideally would be modularised, each component run as a container, and this is where Docker Compose comes in. Docker Compose makes it easy to run multicontainer applications.

Configuration is defined in one or more files, docker-compose.yml by default. A docker-compose.override.yml can also exist which overrides certain parts of the docker-compose.yml and is merged into a single Docker Compose definiton.

A single command is used to manage all services at once, to bring them up, build all the images, shut them all down.

* Docker Compose version: `docker-compose -v`
* Docker Compose help: `docker-compose` adding `help` and `--help` are optional and thus redundant
* Help about a specific command: `docker-compose up --help` - get help on the `up` command

Sample docker-compose.yml:

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