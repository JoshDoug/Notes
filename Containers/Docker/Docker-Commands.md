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
* `docker container rm -f container_name` - stop and remove a container

### Examples

* Create & run a jenkinsci/blueocean container: `docker run -d -p 8080:8080 jenkinsci/blueocean`

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

## Tutorials and Blog Posts

Blog post on creating a container with [SQL Server on Linux in Docker on a Mac with Visual Studio Code](http://thedatafarm.com/data-access/mashup-sql-server-on-linux-in-docker-on-a-mac-with-visual-studio-code/) pretty cool stuff