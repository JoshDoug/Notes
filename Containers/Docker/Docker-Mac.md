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

## Getting Started

Check versions of Docker Engine, Compose, and Machine:

* `docker version` - provides a more complete overview of a version
* `docker --version` - provides just the version number
* `docker-compose version`
* `docker-compose --version`
* `docker-machine version`, same as using `--version`
* Test install by running `docker run hello-world`

## Docker for Mac GUI

### File Sharing

This section of the Docker GUI is for specifying which directories can be shared with a container. To then share a specified directory (or any directory under a specified directory) with a container use the bind mount (-v) feature.

### Advanced

This section allows the number of CPUs and Memory used by Docker to be set, as well as the storage location. By default the CPU number is set to half the number of (logical) processors available on the host machine, Memory defaults to 2GB regardless of the RAM of a machine.

### Proxies

Set a proxy, for example to an image registry. Should read into this.

### Docker Daemon

I'm gonna leave this alone, but basics are covered [here](https://docs.docker.com/docker-for-mac/#docker-daemon).
You can also set custom registires here instead of using Docker Hub or Docker Trusted Registy.

### Reset Section

This provides option to remove all data (but doesn't reset defaults), reset to defaults, and uninstall.
Optionally it's possible to uninstall via the CLI, e.g. if the GUI is not functioning, using this command: `/Applications/Docker.app/Contents/MacOS/Docker --uninstall`.

## TLS Certificates

Haven't read into yet, but covered [here](https://docs.docker.com/docker-for-mac/#adding-tls-certificates).

## [Installing bash completion](https://docs.docker.com/docker-for-mac/#installing-bash-completion)

1. Using homebrew, install bash-completion, or optionally bash-completion@2 with the caveat that bash v4 also needs to be installed.
2. Symlink the following files using these commands:

```bash
ln -s /Applications/Docker.app/Contents/Resources/etc/docker.bash-completion /usr/local/etc/bash_completion.d/docker
ln -s /Applications/Docker.app/Contents/Resources/etc/docker-machine.bash-completion /usr/local/etc/bash_completion.d/docker-machine
ln -s /Applications/Docker.app/Contents/Resources/etc/docker-compose.bash-completion /usr/local/etc/bash_completion.d/docker-compose
```

## [Multi-CPU Architecture Support](https://docs.docker.com/docker-for-mac/multi-arch/)

Docker for Mac can run containers for different Linux architectures, with a few caveats. Covered in the link, because it's complex.

## [Networking](https://docs.docker.com/docker-for-mac/networking/)

* VPN Passthrough
* Port Mapping
* HTTP/HTTPS Proxy Support

### Known Limitations, Use Cases, and Workarounds

* no docker0 bridge on macOS, this interface is actually within `HyperKit`
* cannot ping containers - sad!
* Per-container IP addressing is not possible: the docker (Linux) bridge network is not reachable from the macOS host

### [Use Cases and Workarounds](https://docs.docker.com/docker-for-mac/networking/#use-cases-and-workarounds)

Use cases and workarounds covered by the above link:

* Connecting from a container to a service on the host
* Connecting to a container from macOS

## [File System Sharing](https://docs.docker.com/docker-for-mac/osxfs/)

Info about File System sharing, osxfuse, and potential issues, all covered in the link above.

Performance tuning for volume mounts (shared filesystems) covered [here](https://docs.docker.com/docker-for-mac/osxfs-caching/). I guess I'll read this if I have any performance problems.

## [Logs and Troubleshooting](https://docs.docker.com/docker-for-mac/troubleshoot/#diagnose-problems-send-feedback-and-create-github-issues)

Lots of interesting info in the link above, although the console app info is outdated.

## Creating a docker-machine host

Containers work and run without doing this, so I'm not sure why it's necessary...except for getting environment variables which are most likely necessary to integrate Docker with an IDE.

* [Connecting to the remote Docker Engine API](https://docs.docker.com/docker-for-mac/faqs/#how-do-i-connect-to-the-remote-docker-engine-api)
* [Connecting from a container to a service on the host](https://docs.docker.com/docker-for-mac/faqs/#how-do-i-connect-to-a-container-from-the-mac)