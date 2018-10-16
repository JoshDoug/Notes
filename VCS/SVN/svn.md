# Subversion

* [Apache Subversion Site](https://subversion.apache.org/)
* [Subversions's lackluster documentation page](https://subversion.apache.org/docs/)
* [Subversion Quick Start](https://subversion.apache.org/quick-start)

## Commands

### svnadmin

### svnlook

### svn

* Clone repo:
  * `svn clone https://svn.apache.org/repos/asf/subversion/trunk subversion`
  * `svn co https://svn.apache.org/repos/asf/subversion/trunk subversion`
  * `svn co svn://localhost:3960/repo-name/trunk repo-name`

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

### [Chapter 9: Subversion Complete Reference](http://svnbook.red-bean.com/en/1.7/svn.ref.html)

Complete reference of all subversion commands.