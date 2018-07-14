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

## Vagrant Provisioners

These are scripts defined within the Vagrantfile or externally in a seperate file. By default provisioners are executed the first time a box runs and are used to set up a box for a particular purpose, e.g. install software, set configurations, copy files across to the box. There are also a Docker provisioner and configuration management provisioners for Chef, Puppet, Ansible, and Salt.

Adding Nginx to a box, the base section/code block is included but commented out in the default Vagrantfile:

```Vagrantfile
config.vm.provision "shell", inline: <<-SHELL
  sudo apt-get update
  sudo apt-get install -y nginx
end
```

To do this with an external provisioner file:

```Vagrantfile
config.vm.provision "shell", path: "provisioner/nginx-install.sh"
end
```

and with the provisioner script at the relative path `provisioners/nginx-install.sh`

```Vagrantfile
sudo apt-get update
sudo apt-get install -y nginx
```

These provisions need* to be applied on the first run, if the box has already been booted once then it needs to be removed, `vagrant destroy`, and then run `vagrant up` which will start up a fresh box.

*Vagrant includes options to run these scripts on each boot in case that is required with a `run:always` parameter.

## Vagrant multi-machine Vagrantfile

Typically applications are deployed on mulitple servers, with a database server/container/vm and an application server, this is also possible with Vagrant. These multi-box Vagrant setups can then be connected via a private network.

To connect to a box via SSH the command needs to specify the box name: `vagrant ssh node`

Stripped down example of a mongo and node multi-machine setup:

```Ruby
Vagrant.configure("2") do |config|

  config.vm.define "mongo" do |mongo|
    mongo.vm.box = "bento/ubuntu-16.04"
    mongo.vm.provider "virtualbox" do |vb|
      vb.memory = "512"
    end
    mongo.vm.network "private_network", ip: "192.168.33.20"
    mongo.vm.provision "file", source: "files/mongod.conf", destination: "~/mongod.conf"
    mongo.vm.provision "shell", path: "provisioners/install-mongo.sh"
  end

  config.vm.define "node" do |node|
    node.vm.box = "bento/ubuntu-16.04"
    node.vm.network "forwarded_port", guest: 3000, host: 8080
    node.vm.provider "virtualbox" do |vb|
      vb.memory = "512"
    end
    node.vm.network "private_network", ip: "192.168.33.10"
    node.vm.provision "shell", path: "provisioners/install-node.sh"
  end

  config.vm.box = "bento/ubuntu-16.04" # Should this be here?
end
```
