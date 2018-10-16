# Subversion

* [Apache Subversion Site](https://subversion.apache.org/)
* [Subversions's lackluster documentation page](https://subversion.apache.org/docs/)
* [Subversion Quick Start](https://subversion.apache.org/quick-start)

## Commands

### svnadmin

### svnlook

### svnserve

Start and svn server: `svnserve -d -r /Full/Path/To/Repo/Dirs` where the repo is in the directory that svnserve points to (I think?).
E.g. `svnserve -d -r /Users/jds/Documents/Repos` and there's a repo within called `TestRepo`, with the path `/Users/jds/Documents/Repos/TestRepo`.
This repo can be accessed like other svn repos via the computers IP address (try either localhost, `127.0.0.1`, or the computers local ip address e.g. `192.168.1.15`).
To stop `svnserve` run `killall svnserve` or terminate it from Activity Monitor.

### svn

* `svn help` - typical nix style help command
  * `svn help help`
  * `svn help add`

* Clone repo:
  * `svn checkout https://svn.apache.org/repos/asf/subversion/trunk subversion`
  * `svn co https://svn.apache.org/repos/asf/subversion/trunk subversion`
  * `svn co svn://localhost:3960/repo-name/trunk repo-name`

* List: `svn list svn://localhost:3961/jds-repo/test-project/trunk`

* Status: `svn status` - only provides local info
  * `svn status -u` - add working revision and incoming changes info
  * `svn status -v` - full revision info on every item

* Update:
  * `svn update` - update all code (think this should be run in repo root..)
  * `svn update /path/to/file` - update specific file or directory (not sure if this can be a relative path or just absolute)

* Add:
  * `svn add /path/to/newFile` - add file to svn versioning

* Commit:
  * `svn commit` - update all code (run from repo root or with path to repo root?)
  * `svn commit /path/to/file` - commit specific files instead of every changed file
  * `svn commit -m "Useful commit message"` - add commit message inline (instead of opening default editor)

* Diff:
  * `svn diff` - list differences between local working copy and the repository
  * `svn diff /path/to/file` - list differences between local file and file on the repository

Other commands:

* delete
* rename
* copy

## Hosting an SVN repository

Repository access URLs

| Schema | Access Method |
|--------|---------------|
| `file:///` | Direct repository access (on local disk) |
| `http://` | Access via WebDAV protocol to Subversion-aware Apache server |
| `https://` | Same as `http://`, but with SSL encapsulation (encryption and authentication) |
| `svn://` | Access via custom protocol to an svnserve server |
| `svn+ssh://` | Same as `svn://`, but through an SSH tunnel |

### Repository Structue: Trunks, Tags, and Branches

More of a convention. Project has a main directory called `trunk` which is the primary directory for the project files. Branches are copies of the project where changes are being worked on and are stored in the `branch` directory. Finally the `tag` directory is used to store important snapshots of the repository, such as release versions.

A repository holding multiple projects can be set up in a couple ways. One option is top level `trunk`, `branch`, and `tag` directories which have a directory under them for each project. so the trunk directory has projects 1, 2, and 3, and the branch and tag folders also have directories for projects 1, 2, and 3. The other option is for each project to have a top level folder and then the trunk, branch, and tag directories are within the project folder.

## SVN Book

### [Chapter 2: Basic Usage](http://svnbook.red-bean.com/en/1.7/svn.tour.html)

#### Getting Data into Your Repository

There are two ways to do this: `svn import` and `svn add`.

### [Chapter 9: Subversion Complete Reference](http://svnbook.red-bean.com/en/1.7/svn.ref.html)

Complete reference of all subversion commands.