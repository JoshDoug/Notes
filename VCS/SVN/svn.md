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

## SVN Book

### [Chapter 2: Basic Usage](http://svnbook.red-bean.com/en/1.7/svn.tour.html)

### [Chapter 9: Subversion Complete Reference](http://svnbook.red-bean.com/en/1.7/svn.ref.html)

Complete reference of all subversion commands.