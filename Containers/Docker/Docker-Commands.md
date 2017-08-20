# Basic Docker Commands

## Container Commands

* `docker container` prints the help for the container command, adding `help` and `--help` are optional and thus redundant.
* `docker container run --help` prints the help for run command, here `--help` is necessary.
* `docker container run -it jboss/wildfly` run a jboss container, the `container` command is redundant here.
* `docker container run -d jboss/wildfly` run a detached jboss container
* `docker container run -d --name jboss_web jboss/wildfly` run a detached jboss container and specify the container name
* `docker container stop container_name` - stop a detached container
* `docker container ls` - list currently running containers
* `docker container ls -a` - list all containers, including stopped containers
* `docker container rm container_name` - remove a container

### Old Contaienr Commands - could possibly be deprecated and removed in the future

* `docker ps` - see running containers
* `docker ps -a` - see all containers, including stopped containers

Escape sequence to exit a container without stopping it: `Ctrl-p + Ctrl-q`

Create & run a jenkinsci/blueocean container: `docker run -p 8080:8080 jenkinsci/blueocean`

Blog post on creating a container with [SQL Server on Linux in Docker on a Mac with Visual Studio Code](http://thedatafarm.com/data-access/mashup-sql-server-on-linux-in-docker-on-a-mac-with-visual-studio-code/) pretty cool stuff