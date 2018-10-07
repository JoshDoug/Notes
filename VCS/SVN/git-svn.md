# Git-Svn

Using a handy container to simulate the server hosting the SVN repo.

* [Medium post covering setup of container](https://medium.com/@elle.florio/the-svn-dockerization-84032e11d88d)
* [Docker Hub svn server container](https://hub.docker.com/r/elleflorio/svn-server/)
* [GitHub hosting Docker image details](https://github.com/elleFlorio/svn-docker)
* [Alternative svn container](https://hub.docker.com/r/garethflowers/svn-server/)
* [And related GitHub repo](https://github.com/garethflowers/docker-svn-server)

## Setup

* Create a folder for where all the SVN repos will be stored and cd into it (so the `pwd` docker volume command picks it up)
* Start svn-server: ```docker run -d -p 80:80 -p 3960:3960 -v `pwd`/:/home/svn --name svn-server elleflorio/svn-server```
* Setup svn admin password: `docker exec -t svn-server htpasswd -b /etc/subversion/passwd user pass` (substitue a username for user and a password for pass)
* `docker pause svn-server`
* `docker unpause svn-server`
