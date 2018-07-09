# Vagrant

Installation, just install VirtualBox and Vagrant.

* [Vagrant](https://www.vagrantup.com/)
* [Find Boxes](https://app.vagrantup.com/boxes/search)

## Running your first box

* Create a directory for the environment and change to the directory
* Create a `VagrantFile` using the `init` command, e.g. `vagrant init ubuntu/bionic64` or `vagrant init generic/fedora28`
  * Vagrant files are simple Ruby programs
* Run `vagrant up`, this will run the virtual machine and, if necessary, download the vm image first

## Vagrant commands

* Check status: `vagrant status` - directory specific
* Check status of all vagrant boxes: `vagrant global-status`
* Start a box: `vagrant up`
* Suspend a box: `vagrant suspend`
* Forcefully shut down: `vagrant halt`
* Remove a vm: `vagrant destroy`
* SSH into a vm: `vagrant ssh`, when SSH'd in running `exit` will return you to the host cli
* Update a vm: `vagrant box update`, vagrant can prompt that an updates available
* Restart a vm: `vagrant reload`
* Vagrant commands can be used on machines using their id without being in the same directory, e.g.
  * To stop a vm: `vagrant halt 1a2b3c4d`
  * To remove a vm: `vagrant destroy 1a2b3c4d`