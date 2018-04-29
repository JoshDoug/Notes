# Docker

General information about what Docker is, how containers work, what containers are for.

* [What is Docker?](https://www.docker.com/what-docker)
* [Docker CLI Reference Guide](https://docs.docker.com/engine/reference/commandline/cli/), and [Engine API](https://docs.docker.com/engine/api/)
* [Docker Labs](https://github.com/docker/labs/)
* [Documentation Glossary](https://docs.docker.com/glossary/)
* [Reference Documentation](https://docs.docker.com/reference/)
* [Samples](https://docs.docker.com/samples/)
* [Docker Engine API](https://docs.docker.com/develop/sdk/)

## Tutorials and Blog Posts

* Blog post on creating a container with [SQL Server on Linux in Docker on a Mac with Visual Studio Code](http://thedatafarm.com/data-access/mashup-sql-server-on-linux-in-docker-on-a-mac-with-visual-studio-code/) pretty cool stuff
* Docker 101: [Introduction to Docker](https://www.youtube.com/watch?v=V9IJj4MzZBc) on YouTube.
* [Play with Docker Classroom](http://training.play-with-docker.com/)

## [What is Docker](https://www.docker.com/what-docker)

Docker is a software container platform. According to Docker's marketing speel it helps do the following:

* Provides a consistent environment for collaboration and helps avoid "Works on my machine"
* Run and manage apps side-by-side in isolated containers to get better compute density
* Build agile software delivery pipelines to ship new features faster, more securely, and with confidence for both Linux, Windows Server, and Linux-on-mainframe apps.

What is a container?

Containers are a way to isolate, package, and run software on a shared operating system. Unlike VMs, containers don't bundle a full OS and virtualise it, this makes them more lightweight and efficient but with many of the advantages of VMs. The most important aspect is that the software always runs the same, regardless of where it's deployed. See 'What is a Container' section below.

Docker for Developers

* Test and debug apps in consistent environments that mimic production with minimal setup
* Any language or tech stack
* Reduce onboarding time installing and configuring software

Docker for [Ops and Sys Admins](https://www.docker.com/itpro)

* Docker streamlines software delivery
* Scale applications in real time
* Automate the shipping and deployment of apps securely
* Ship more frequently
* And [more](https://www.docker.com/what-docker#/operators)

Docker for Enterprise - See Enterprise doc.

## [What are Docker's Use Cases](https://www.docker.com/use-cases)

* Modernise traditional apps
* Devops (CI/CD) automation and integration
* Hybrid Cloud
* Microservices go hand in hand with conatiners
* Infrastructure optimisation

## [What is a Container](https://www.docker.com/what-container)

Could probably be a seperate doc.

Container primitives, namespaces, cgroups, etc.

containerd, runC, LXC, etc.

## [Getting Started](https://docs.docker.com/get-started/)

### Part 1: Orientation

Mostly verbatim from Dockers documentation:

"An **image** is a lightweight, stand-alone, executable package that includes everything needed to run a piece of software, including the code, a runtime, libraries, environment variables, and config files."

"A **container** is a runtime instance of an image - what the image becomes in memory when executed. It runs completely isolated from the host environment by default, only accessing host files and ports if configured to do so."

Containers run apps natively on the host machine’s kernel. They have better performance characteristics than virtual machines that only get virtual access to host resources through a hypervisor. Containers can get native access, each one running in a discrete process, taking no more memory than any other executable.

Containers vs. Virtual Machines

Virtual machines run guest operating systems. This is resource intensive, and the resulting disk image and application state is an entanglement of OS settings, system-installed dependencies, OS security patches, and other easy-to-lose, hard-to-replicate ephemera.

Containers can share a single kernel, and the only information that needs to be in a container image is the executable and its package dependencies, which never need to be installed on the host system. These processes run like native processes, and you can manage them individually by running commands like `docker ps`—just like you would run ps on Linux to see active processes. Finally, because they contain all their dependencies, there is no configuration entanglement; a containerized app “runs anywhere.”
