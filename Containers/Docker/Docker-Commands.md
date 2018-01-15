# Basic Docker Commands

## Container Commands

* `docker container` prints the help for the container command, adding `help` and `--help` are optional and thus redundant.

* `docker container run --help` prints the help for run command, here `--help` is necessary.
* `docker container run -it jboss/wildfly` run a jboss container, the `container` command is redundant here.
* `docker container run -d jboss/wildfly` run a detached jboss container
* `docker container run -d --name jboss_web jboss/wildfly` run a detached jboss container and specify the container name
* `docker container run -it --name jboss_web jboss/wildfly bash` run a detached jboss container and specify the container name and the command to run is bash, instead of the default command for the container, which in this case would start wildfly.
* `docker container run -d --name web -P jboss/wildfly` - create a container and expose a port for it, the local port is random, the container port will default to 8080 (i think?), or maybe the container can specify its own default.
* `docker container run -d --name web -p 8080:8080 jboss/wildfly` - specify the port mapping on the container
* `docker container run -d --name web -p 8080:8080 -v /path/to/volume/webapp.war:/opt/jboss/wildfly/standalone/deployments/webapp.war jboss/wildfly` - specify the port mapping on the container

* Neat trick for setting the directory for the local volume:

```docker
docker container run -d --name web -p 8080:8080 -v `pwd`/webapp.war:/opt/jboss/wildfly/standalone/deployments/webapp.war jboss/wildfly
```

* `docker container logs container_name` - shows the logs for the specified container - not sure how these logs are generated and specified by the container though - how would you get tomcats wrapper.log? Probably just catches everything that goes to stdout and stderr?
* `docker container logs container_name -f` - tail the log

* `docker container stop container_name` - stop a detached container
* `docker container ls` - list currently running containers, also useful for checking port mappings
* `docker container ls -a` - list all containers, including stopped containers
* `docker container rm container_name` - remove a container
* `docker container rm container_name other_container another_container` - remove multiple containers
* `docker system prune` - remove all stopped containers
* `docker container rm -f container_name` - stop and remove a container

### Examples

* Create & run a jenkinsci/blueocean container: `docker run -d -p 8080:8080 jenkinsci/blueocean`

#### PHP

* [PHP on Docker Cloud](https://store.docker.com/images/php)
* [Integration with PhpStorm](https://confluence.jetbrains.com/display/PhpStorm/Docker+Support+in+PhpStorm)

Docker provides several 'offical image' types for PHP, a CLI version, ZTS enabled, on Debian Jessie, with FPM enabled, with Apache httpd included, and several combinations of those options (all options include the CLI). These are provided for major versions 5.6, 7.0, 7.1, and 7.2.

The basic PHP & Apache install work well and require minimal configuration. Linking to a database container may involve some basic work.

Setting up debug support (using xDebug) with PhpStorm requires a few extra steps:

* Configure Docker within PhpStorm, set it to use a Dockerfile. Configure the Dockerfile as needed, e.g. bind ports `8080:80`, bind mounts `pwd/src:/var/www/html`, set an image tag and container name. That seems to be the minimum configuration necessary.
* Next add a Docker file that sets up xDebug and configures it
* Make sure that the Xdebug browser extension is installed and that PhpStorm is listening
* At this point if the container is running and a break point is enabled it should just work, the container can be run in normal mode and then PhpStorm will automatically switch to debug mode.

```Dockerfile
FROM php:7.1-apache

RUN pecl install xdebug-2.5.5 \
    && docker-php-ext-enable xdebug

# Set up debugger
RUN echo "xdebug.remote_enable=1" >> /usr/local/etc/php/php.ini

# Provide host ip, on a mac the special dns name can be used:
# https://docs.docker.com/docker-for-mac/networking/#there-is-no-docker0-bridge-on-macos
# Optionally this could be set as an environment variable for better cross platform compatibility
RUN echo "xdebug.remote_host=docker.for.mac.localhost" >> /usr/local/etc/php/php.ini

# COPY src/ /var/www/html/ - only for production
# Add `-v src/:/var/www/html` to PhpStorm's Docker runtime configuration arguments, not including the backticks
```

Note: Possible alternative to using the special docker dns name would be the xdebug `xdebug.remote_connect_back=1` option which gets the host ip from the headers, which has possible safety issues but should be fine on a local development environment. See [xdebug remote connect back documentation](https://xdebug.org/docs/all_settings#remote_connect_back).

#### MariaDB

* [Docker Store - MariaDB page, scroll down for ReadMe](https://store.docker.com/images/mariadb)

* ```docker container run -d --name test-mariadb --env-file env.list -p 3306:3306 -v `pwd`:/docker-entrypoint-initdb.d mariadb:latest```
* Shared volume contains a DB export script on the host, which is automatically picked up and executed by mariadb when in the `docker-entrypoint-initdb.d` directory in the container.
* The `env.list` contains all the environment variables, instead of manually setting them each time. It can be in the same directory that's shared with the container because it will be ignored (anything without a `.sql`, `.sh`, or `.sql.gz` file extension is ignored), or in another folder, specified with a relative path
* The port forwarding is only necessary when remotely accessing the DB (e.g. via the host), it's not necessary when using other containers in conjunction with mariadb as they should be linked differently.

Env list:

```conf
# MariaDB environment variables for test setup
MYSQL_ROOT_PASSWORD=example-password # Replace with proper password
MYSQL_DATABASE=example-db-name
MYSQL_USER=dbuser # Non-root user
MYSQL_PASSWORD=dbpassword # Replace with proper password
```

#### Container Orchestration - PHP & MariaDB

If you're working with containers your probably want to be working with everything in containers. Of course that's going to involve multiple containers because working with everything in a single container kind of ruins the point. Using the above examples it would make sense to have a database such as MariaDB running in a container and accessible from the PHP/Apache container.

With the example below there is an application container containing the PHP code and Apache httpd, this exposes port 80 to port 8080 on the host. There is also the database container, but this doesn't need to expose any ports to the host as only the application will be accessing it and they share a docker created overlay network (i think?). Note that the volumes for each start with `./`, relative paths require this otherwise `docker-compose` believes they are named volumes which require some extra configuration.

Only the PHP/Apache httpd container requires a Dockerfile, the database can be configured with the `env.list`, database script, and the compose file. The PHP/Apache httpd Dockerfile includes an extra line from before, `docker-php-ext-install pdo_mysql` to install the PDO drivers for MySQL.

The `docker-compose.yml` file:

```YAML
version: '3'
services:
  web:
    build: .
    ports:
     - "8080:80"
    volumes:
     - ./src/:/var/www/html/
  db:
    image: "mariadb:latest"
    volumes:
      - ./db-data:/docker-entrypoint-initdb.d
    env_file: env.list
```

The Dockerfile for PHP and Apache httpd:

```Dockerfile
FROM php:5.6-apache

RUN pecl install xdebug-2.5.5 \
    && docker-php-ext-enable xdebug \
    && docker-php-ext-install pdo_mysql

# Set up debugger
RUN echo "xdebug.remote_enable=1" >> /usr/local/etc/php/php.ini

# Provide host ip, on a mac the special dns name can be used
RUN echo "xdebug.remote_host=docker.for.mac.localhost" >> /usr/local/etc/php/php.ini

# COPY src/ /var/www/html/ - only necessary when creating an image, not useful for general development
```

The environment variable file for the database, with demo passwords (replace with actual passwords):

```conf
# MariaDB environment variables for test setup
MYSQL_ROOT_PASSWORD=my-secret-pw
MYSQL_DATABASE=explorecalifornia
MYSQL_USER=dbuser
MYSQL_PASSWORD=dbpassword
```

TODO/TKTK : add a basic corresponding project with a simple database and link the repo here so that setup involves cloning the repo and running `docker-compose.yml` to demonstrate it.

Note: When using Compose it isn't necessary to add the runtime arguments to PhpStorm's runtime configuration.

Note: With PhpStorm, if docker-compose will not run then check `Preferences > Docker > Tools` and check the entry for docker-compose, if it is just `docker-compose` then try specifying the absolute path (run `which docker-compose`).

### Old Contaienr Commands - could possibly be deprecated and removed in the future

* `docker ps` - see running containers
* `docker ps -a` - see all containers, including stopped containers

## Image Commands

Creating a docker image, docker image commands, and writing a Dockerfile.

* `docker image` prints the help for the image command, adding `help` and `--help` are optional and thus redundant.
* `docker pull store/oracle/serverjre:8` pull the specified image down so it is stored locally ready for use
* `docker image ls` list current images
* `docker image build --help` get help for the build command
* `docker image build -t helloworld .` build the dockerfile in the current directory with the tag helloworld, this image can then be run as a container as any other image would be.
* `docker build -t helloworld .` - shorter and also works, `build` part of command is redundant
* `docker build -t helloworld:2 .` - build and tag the 2nd version of the image helloworld
* `docker history helloworld` see how the image helloworld was built

### Dockerfile Reference

* FROM - this has to be the first instruction, which is not a comment.
* COPY - Copy files or directories to the container filesystem
* ADD - Copy a file, such as a tar file and then extract it, e.g. `ADD app.tar.gz /opt/var/myapp`
* EXPOSE - network ports on which the container is listening
  * E.g. `EXPOSE 9990`
  * This only exposes the port for the container, when running the container -P or -p are still necessary to publish the host port
* VOLUME - creates a mount point with the specified name
  * `VOLUME /opt/couchbase/var` - set up the mount point
  * `docker container run -v ~/data:/opt/couchbase/var image_name`
* RUN - useful for updating a container, installing a package, running a script on the container, etc. Examples:
  * `RUN apt-get update && apt-get install -y git`
  * `RUN /opt/jboss/wildfly/bin/add-user.sh admin Admin#007 - silent`
* ENTRYPOINT - configures the container executable, defaults to `/bin/sh -c`, can be overridden from CLI with --entrypoint
  * ENTRYPOINT ["/entrypoint.sh"]
* USER - sets the username or UID to use when running the image
* HEALTHCHECK - performs a healthcheck on the application inside the container
  * `HEALTHCHECK --interval=5s timeout=3s CMD curl --fail http://localhost:8091/pools || exit 1`
  * In the example a check will be made on the couchbase container every 5 seconds, if after 3 seconds the container doesn't return a result mark the container as unhealthy.
* CMD - the command the container should run, be it starting a service or just running a UNIX tool, the last CMD in the dockerfile overwrites any prior CMD commands, including on the image pulled into the Dockerfile, and can itself be overriden when a container is run from the CLI.

Dockerfile reference [documentation](https://docs.docker.com/engine/reference/builder/).

```Dockerfile
FROM alpine

CMD echo "Hello World"
```

## Tagging and Sharing Docker Images

Tag an image: `docker image tag helloworld:2 helloworld:latest` - tag v2 of helloworld as the latest version

Push an image to docker hub:

* Create an account on docker hub.
* Login to docker hub via CLI using `docker login` and following prompts.
* Tag an image with a namespace: `docker image tag helloworld:2 joshdoug/helloworld:latest`
* Push image: `docker push joshdoug/helloworld:latest`

Using a local registry:

* Run registry container: `docker run -d -p 5000:5000 --restart always registry registry:2.6.0`
* Tag image: `docker tag helloworld:latest localhost:5000/joshdoug/helloworld:latest`
  * The format for the tag is registry:namespace:image:tag
* Push the image to the local registry: `docker image push localhost:5000/joshdoug/helloworld:latest`

## Other shortcuts and commands

Escape sequence to exit a container without stopping it: `Ctrl-p + Ctrl-q`