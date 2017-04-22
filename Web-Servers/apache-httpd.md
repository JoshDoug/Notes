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

## Configuration
