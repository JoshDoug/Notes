# Apache HTTP Server (httpd) 2.4
Info covering the Apache httpd server.

## Installing
httpd can be installed in a number of ways:
* macOS - compiled, pre-installed system version (often outdated), homebrew install, MAMP
* Windows - why?
* Linux - compiled, installed via package manager (either seperately or part of a group install on e.g. CentOS)

### macOS
Using brew, just run the typical `brew install httpd24` with additional options added.
If already installed with brew, you can check the options currently used by running `brew info httpd24` and the options will be listed at the top of the output, e.g. `Built from source on 2017-04-17 at 00:10:13 with: --with-privileged-ports --with-http2`.
Replace the 24 in httpd24 with whatever the current version is, or however it is later versioned in homebrew.

### Windows
Apache covers downloading binaries here: https://httpd.apache.org/docs/current/platform/windows.html
Compiling from scratch is covered here: https://httpd.apache.org/docs/current/platform/win_compiling.html

Might be easier to just use IIS.

### Linux
RPM based systems: https://httpd.apache.org/docs/current/platform/rpm.html
Compiling from scratch: https://httpd.apache.org/docs/current/install.html

[Distro Default Layouts](https://wiki.apache.org/httpd/DistrosDefaultLayout) - The location and naming of configuration files and the application itself can differ between distros, so this page helpfully summaries the defaults and distro conventions.

### Install Options (from brew, there may be additional options)
Options given by running `brew options httpd24`:
```
--with-http2
	Build and enable the HTTP/2 shared Module
--with-ldap
	Include support for LDAP
--with-mpm-event
	Use the Event Multi-Processing Module instead of Prefork
--with-mpm-worker
	Use the Worker Multi-Processing Module instead of Prefork
--with-privileged-ports
	Use the default ports 80 and 443 (which require root privileges), instead of 8080 and 8443
```


Preworker, MPM Event, MPM Worker:
Confusing
* https://httpd.apache.org/docs/2.4/mpm.html
* https://serverfault.com/questions/231628/apache-mpms-worker-vs-prefork
* https://serverfault.com/questions/383526/how-do-i-select-which-apache-mpm-to-use
* http://www.binarytides.com/apache-mpm-php-server-api/
* https://www.liquidweb.com/kb/apache-mpms-explained/


## Configuration


## Management

### Logs
Located at: `/usr/local/var/log/apache2/error_log` when using brew, useful for diagnosing issues.