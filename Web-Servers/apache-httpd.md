# Apache HTTP Server (httpd) 2.4

Info covering the Apache httpd server.

## [Documentation](https://httpd.apache.org/docs/current/)

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

Apache covers downloading binaries [here](https://httpd.apache.org/docs/current/platform/windows.html)
Compiling from scratch is covered [here](https://httpd.apache.org/docs/current/platform/win_compiling.html)

Might be easier to just use IIS.

### Linux

Install on [RPM based systems](https://httpd.apache.org/docs/current/platform/rpm.html)
Compiling Unix-like systems from scratch: [Compiling httpd](https://httpd.apache.org/docs/current/install.html)

[Distro Default Layouts](https://wiki.apache.org/httpd/DistrosDefaultLayout) - The location and naming of configuration files and the application itself can differ between distros, so this page helpfully summaries the defaults and distro conventions.

### Install Options (from brew, there may be additional options)

Options given by running `brew options httpd24`:

```config
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

Preworker, MPM Event, MPM Worker, confusing:

* [Apache MPM Docs](https://httpd.apache.org/docs/2.4/mpm.html)
* [Serverfault answer - MPM worker vs prefork](https://serverfault.com/questions/231628/apache-mpms-worker-vs-prefork)
* [Serverfault answer - which mpm to use](https://serverfault.com/questions/383526/how-do-i-select-which-apache-mpm-to-use)
* [Binary Tides - Apache MPM PHP Server API](http://www.binarytides.com/apache-mpm-php-server-api/)
* [Liquid Web - Apache MPMs explained](https://www.liquidweb.com/kb/apache-mpms-explained/)

## Configuration

Typically configured using http.conf and then subconfig files that can be included in a subdirectory, e.g. instead of having several vhosts listed in httpd.conf it is typical to create a vhosts directory and include it in httpd.conf.

### httpd.conf

### vhosts

### Directives

A set of configuration rules to change and add functionality to the http server, typically involve enabling additional modules, e.g. mod_rewrite.

* [Directive Index](https://httpd.apache.org/docs/current/mod/directives.html)
* [Directive Dictionary](https://httpd.apache.org/docs/current/mod/directive-dict.html)
* [Directive Quick Reference](https://httpd.apache.org/docs/current/mod/quickreference.html)

#### mod_rewrite

It could make sense to split directives like this into their own files.
This module helps clean up URL/URIs by using rule-based rewrites to rewrite and serve a requested URL on the fly. It can be used to:

* map a URL to a filesystem path
* redirect one URL to another URL
* invoke an internal proxy fetch
* can be per server (httpd.conf), per virtual host, or per directory (.htaccess files and [`<Directory>`](https://httpd.apache.org/docs/current/mod/core.html#directory) blocks)

Detailed Apache mod_rewrite [documentation](https://httpd.apache.org/docs/current/rewrite/).

* [mod_rewrite reference documentation](https://httpd.apache.org/docs/current/mod/mod_rewrite.html)
* [Introduction to regular expressions and mod_rewrite](https://httpd.apache.org/docs/current/rewrite/intro.html)
* [Using mod_rewrite for redirection and remapping of URLs](https://httpd.apache.org/docs/current/rewrite/remapping.html)
* [Using mod_rewrite to control access](https://httpd.apache.org/docs/current/rewrite/access.html)
* [Dynamic virtual hosts with mod_rewrite](https://httpd.apache.org/docs/current/rewrite/vhosts.html)
* [Dynamic proxying with mod_rewrite](https://httpd.apache.org/docs/current/rewrite/proxy.html)
* [Using RewriteMap](https://httpd.apache.org/docs/current/rewrite/rewritemap.html)
* [Advanced techniques](https://httpd.apache.org/docs/current/rewrite/advanced.html)
* [When NOT to use mod_rewrite](https://httpd.apache.org/docs/current/rewrite/avoid.html)
* [RewriteRule Flags](https://httpd.apache.org/docs/current/rewrite/flags.html)
* [Technical details](https://httpd.apache.org/docs/current/rewrite/tech.html)

##### mod_rewrite reference documentation

###### Logging

Shouldn't be set unless debugging because it can drastically slow down a server.

## Management/Using httpd

### Starting & Stopping

* [Starting](https://httpd.apache.org/docs/current/invoking.html)
* [Stopping & Restarting](https://httpd.apache.org/docs/current/stopping.html)

Or using brew: `brew services httpd24 run|start|stop|restart`

If Listen is set for port 80 or any port below 1024 then httpd will need to be launched with root priveledges and httpd will run as root, but any child processes spawned will run as a less priveleged user.

The location of the configuration file used is set at compile time, but a different file can be passed when starting up e.g.:
`/usr/local/apache2/bin/apachectl -f /usr/local/apache2/conf/alternative-httpd.conf`

### Logs

Located at: `/usr/local/var/log/apache2/error_log` when using brew, useful for diagnosing issues.