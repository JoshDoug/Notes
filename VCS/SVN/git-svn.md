# Git-Svn

Using a handy container to simulate the server hosting the SVN repo.

* [Medium post covering setup of container](https://medium.com/@elle.florio/the-svn-dockerization-84032e11d88d)
* [Docker Hub svn server container](https://hub.docker.com/r/elleflorio/svn-server/)
* [GitHub hosting Docker image details](https://github.com/elleFlorio/svn-docker)
* [Alternative svn container](https://hub.docker.com/r/garethflowers/svn-server/)
* [And related GitHub repo](https://github.com/garethflowers/docker-svn-server)
* [Archived blog post: Installation and Configuration of SVN](https://web.archive.org/web/20110314195306/http://www.duchnik.com:80/tutorials/vc/installing-and-configuring-svn-on-centos)
* [Archived blog post: SVN Command Reference & Repo Setup Steps](https://web.archive.org/web/20110314195306/http://www.duchnik.com:80/tutorials/vc/installing-and-configuring-svn-on-centos)
* [Git Docs: git-svn](https://git-scm.com/docs/git-svn)
* [Git Book: Git and Subversion](https://git-scm.com/book/en/v1/Git-and-Other-Systems-Git-and-Subversion)
* [Atlassian: git-svn tips & tricks](https://www.atlassian.com/blog/git/git-svn-tips-and-tricks)

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
    * or maybe `git svn clone svn://127.0.0.1:3961/jds-repo/test-project . -s`
* Start adding some files:
  * `echo "Hello World" > test.txt` in the svn working dir (locally copy)
  * `svn status` to see the current state of the repo
  * `svn add test.txt` to add the file to the repo
  * `svn commit -m "Add test file"` to commit the file with a commit message
  * `git svn rebase` to pull that change into the `git svn` repo. **Not totally sure this is the right/best option but it works.**

## Using git-svn

Cloning the repo:

* `git svn clone uri/to/repo` - this clones (or inits and fetchs) the repo. Depending on the size of the repo this can take a long time, for a repo with 100s or 1000s of commits it could take several hours or days
* `git svn clone uri/to/repo -T trunk -b branches - t tags` - tells git the layout of the repo, if these directories are named differently then change accordingly
* `git svn clone uri/to/repo -s` - a shorthand for the above if the repo follows the standard directory layout

Working locally:

* `git svn commit -am "Add and commit some test file"`

Pull incoming changes:

* `git svn rebase` - this is similar to a `git pull` when working with `git` or `svn update` when working with `svn`, you should stash or commit local changes before doing this
* `git svn fetch` - fetches the data but doesn't update the local commits, this doesn't seem to cause issues with uncommited changes in the local working directory, the changes can then be merged using a rebase, e.g. in the IntelliJ VCS Git Log section

Pushing to the remote:

* `git svn dcommit` - do something?

Ignoring files:

* `git svn show-ignore` - show any files currently ignored by svn
* `git svn create-ignore` - add any files currently ignored by svn to a `.gitignore`, probably don't want to commit this though

### Simple git svn workflow

* TKTK: Stash or commit any local changes: `git stash` or `git svn commit`
* Update local working copy: `git svn rebase`
* Make changes
* Commit changes: `git svn commit`
* Push changes: `git svn dcommit`

* Might be an idea to alias a command or script that covers `git stash && git svn rebase && git stash pop`