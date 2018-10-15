# Git-Svn

Using a handy container to simulate the server hosting the SVN repo.

* [Medium post covering setup of container](https://medium.com/@elle.florio/the-svn-dockerization-84032e11d88d)
* [Docker Hub svn server container](https://hub.docker.com/r/elleflorio/svn-server/)
* [GitHub hosting Docker image details](https://github.com/elleFlorio/svn-docker)
* [Alternative svn container](https://hub.docker.com/r/garethflowers/svn-server/)
* [And related GitHub repo](https://github.com/garethflowers/docker-svn-server)

## Setup elleFlorio

* Create a folder for where all the SVN repos will be stored and cd into it (so the `pwd` docker volume command picks it up)
* Start svn-server: ```docker run -d -p 80:80 -p 3960:3960 -v `pwd`/:/home/svn --name svn-server elleflorio/svn-server```
* Setup svn admin password: `docker exec -t svn-server htpasswd -b /etc/subversion/passwd user pass` (substitue a username for user and a password for pass)
* `docker pause svn-server`
* `docker unpause svn-server`
* Check connection: `svn info svn://localhost:3960` - this will fail if there are no repos, but the error message should indiciate whether the client successfully connected to the container, might also need to try `127.0.0.1` instead of `localhost`, to check a specific project use `svn info svn://127.0.0.1:3960/Test2` or via `http`: `svn info http://127.0.0.1/svn/Test2` (http requires the `/svn/` path included for some reason)
* Create a repo locally with `svnadmin create Test`
* Create a repo via the container (only works for garethflowers svn server container): `docker exec -it container-name svnadmin create repo-name`
* Clone repo with `git svn clone svn://127.0.0.1:3960/Test2` or over HTTP with a username `git svn clone http://127.0.0.1/svn/Test2 --username jds`

## Setup using Gareth Flowers Container

* Create a folder that will be shared with the container volume holding the svn repos and `cd` into it
* Run ```docker run -d -p 3961:3690 -v `pwd`/:/var/opt/svn --name alt-svn-server garethflowers/svn-server```
* Create a repo using the container: `docker exec -it alt-svn-server svnadmin create jds-repo`
* This will show up in the shared volume as a folder called `jds-repo` with svn's default repo files, this means multiple repos can be created in the volume root
* Test repo connection: `svn info svn://localhost:3961/jds-repo` this should output some info about the repo confirming the connection worked
* Add svn user in the container:
  * In `conf/svnserve.conf` uncomment the lines for `anon-access = read`, `auth-access = write`, and `password-db = passwd`
  * In `conf/passwd` add a user and password following the examples in the file, e.g. `josh = examplePassword`
* Create the project directories:
  * Create the project root: `svn mkdir svn://localhost:3961/jds-repo/test-project -m "Create project root" --username jds`
  * Create the trunk, tags, and branches directories with this format: `svn mkdir svn://localhost:3961/jds-repo/test-project/trunk -m "Create project trunk"`
  * Note when creating the trunk the username didn't need to be supplied again
* Clone project:
  * Create the base project dir and cd into it: `mkdir test-project && cd test-project`
  * Clone (or in svn lingo 'checkout') the project trunk: `svn co svn://localhost:3961/jds-repo/test-project/trunk .`
  * Instead of the whole project just the trunk is cloned as that's where the actual project code will live, the `.` at the end avoids the trunk directory being created locally
  * The local base project dir should now contain a `.svn` directory
  * Clone the project with `git svn`: `git svn clone svn://127.0.0.1:3961/jds-repo/test-project/trunk .` - these seems to need the localhost ip instead of hostname.
* Start adding some files:
  * `echo "Hello World" > test.txt` in the svn working dir (locally copy)
  * `svn status` to see the current state of the repo
  * `svn add test.txt` to add the file to the repo
  * `svn commit -m "Add test file"` to commit the file with a commit message
  * `git svn rebase` to pull that change into the `git svn` repo. **Not totally sure this is the right/best option but it works.**