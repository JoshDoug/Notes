# Docker for Mac

* Installing [Docker for Mac](https://docs.docker.com/docker-for-mac/install/) - includes download links
* [Docker for Mac vs Docker Toolbox](https://docs.docker.com/docker-for-mac/docker-toolbox/)
* Docker for Mac [Documentation](https://docs.docker.com/docker-for-mac/)
* [FAQ](https://docs.docker.com/docker-for-mac/faqs/)
* [Latest Docker for Mac release notes](https://docs.docker.com/docker-for-mac/release-notes/)
* [Docker for Mac forums](https://forums.docker.com/c/docker-for-mac)
* [Docker for Mac GitHub issues](https://github.com/docker/for-mac/issues)

## Installing Docker for Mac

For older Macs that don't support certain CPU virtualisation instructions Docker Toolbox can be used.
Fully uninstalling Docker Toolbox is covered [here](https://docs.docker.com/toolbox/toolbox_install_mac/#how-to-uninstall-toolbox).

Otherwise it is straightforward to install Docker for Mac with the .dmg downloaded from this [link](https://download.docker.com/mac/stable/Docker.dmg).

## Creating a docker-machine host

Containers work and run without doing this, so I'm not sure why it's necessary...except for getting environment variables which are most likely necessary to integrate Docker with an IDE.

* [Connecting to the remote Docker Engine API](https://docs.docker.com/docker-for-mac/faqs/#how-do-i-connect-to-the-remote-docker-engine-api)
* [Connecting from a container to a service on the host](https://docs.docker.com/docker-for-mac/faqs/#how-do-i-connect-to-a-container-from-the-mac)

## STUB - consider extending or removing