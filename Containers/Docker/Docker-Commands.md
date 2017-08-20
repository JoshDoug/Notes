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

### Old Contaienr Commands - could possibly be deprecated and removed in the future

* `docker ps` - see running containers
* `docker ps -a` - see all containers, including stopped containers

Escape sequence to exit a container without stopping it: `Ctrl-p + Ctrl-q`

Create & run a jenkinsci/blueocean container: `docker run -p 8080:8080 jenkinsci/blueocean`

Blog post on creating a container with [SQL Server on Linux in Docker on a Mac with Visual Studio Code](http://thedatafarm.com/data-access/mashup-sql-server-on-linux-in-docker-on-a-mac-with-visual-studio-code/) pretty cool stuff