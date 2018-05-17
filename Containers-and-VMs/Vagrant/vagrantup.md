# Vagrant

Installation, just install VirtualBox and Vagrant.

## Running your first box

* Create a directory for the environment and change to the directory
* Create a `VagrantFile` using the `init` command, e.g. `vagrant init ubuntu/bionic64`
* Run `vagrant up`, this will run the virtual machine and, if necessary, download the vm image first

## Vagrant commands

* Check status: `vagrant status` - directory specific
* Check status of all vagrant boxes: `vagrant global-status`
* To stop a vm: `vagrant halt 1a2b3c4d`
* To remove a vm: `vagrant destroy 1a2b3c4d`