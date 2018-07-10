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

## Vagrant Synced Folders

Folders between the host and vagrant box can be synced by configuring the VagrantFile, by default the folder containing the Vagrantfile is shared with the `/vagrant' folder on the vm.
To add a synced folder edit the Vagrantfile: `config.vm.synced_folder "../test-data", "/vagrant_data"`.

## Vagrant Networking

The first networking option in the Vagrantfile is an insecure portforward, instead the latter options specifying `127.0.0.1`, localhost, or a specific IP address are safer to use: `config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"`.
Additionally to setup a private host only network use: `config.vm.network "private_network", type: "dhcp"`, this will create a private network with Virtualbox(?) accessible only via the host.

## Vagrant Providers

This section of the Vagrantfile allows for hypervisor specific configurations and some generic configurations, such as setting CPU and memory limits.
An example of a provider specific config, a graphical shell can be added for virtualbox under the Vagrantfile VirtualBox provider settings:

```Vagrantfile
config.vm.provider "virtualbox" do |vb|
  vb.gui = true
  vb.customize["modifyvm", :id, "--vram", "16"]
end
```

The username and password for the graphical shell are both `vagrant`.

There can be some additional options required when using different providers.
