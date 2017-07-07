# Personal computer configuration.

This is my personal MacBook configuration. There are many like it, but
this one is mine.

For that reason it's largely set up for my particular needs. If you want
to use it yourself I'd recommend reading through it first. Remove as
much as possible and build up, making changes as you go, so it fits your
needs.

### Set up

Run the bootstrap script. This will ensure gcc,
[Homebrew](http://brew.sh/), and [Ansible](http://docs.ansible.com/) are
installed:

    $ ./bootstrap.sh
    $ ansible-playbook local.yml -K

The `-K` flag means that Ansible will prompt you for your sudo password
before it executes the playbook.

If it's your first time, go brew some coffee or tea because this will take a while

### Using Vagrant to configure and run a virtual machine:

First, Download: 
	vagrant - [https://www.vagrantup.com/downloads.html](Link URL)
	virtualbox - [https://www.virtualbox.org/wiki/Downloads](Link URL)
	download the extension package for virtualbox in the above link as well.

Vagrant is used to script the creation of a virtua machine (in our case using the virtualbox platform) and enables preconfiguration of it.
The included VagrantFile will start a MacOS Siera virtualbox and run the configuration script (bootstrap4vagrant.sh).

once you have downloaded all the necessary softwares run (in this folder):

    $ vagrant up

This will create and configure the virtual machine according to the vagrant file.
Important: on the first run of "vagrant up" vagrant will downloaded the base image for the virtual machine, also known as "box".
In our case of using the box for macos it may take about 2 hours.

Currently the vagrantfile will only install on the virtual machine developer tools, homebrew and ansible.

Once the virtual machine is up, you can ssh to it with:

    $ vagrant ssh

To actually run the ansible-playbook run the following commands on the virtual machine:

    $ export PATH=/usr/local/bin:$PATH

    $ cd /vagrant

    $ ansible-playbook local.yml

If you wish to interact with the virtual machine with a GUI run the following shell command on the virtual machine:

    $ sudo /System/Library/CoreServices/RemoteManagement/ARDAgent.app/Contents/Resources/kickstart -activate -configure -access -off -restart -agent -privs -all -allowAccessFor -allUsers

On your machine in the Finder press CMD+K and type in:
vnc://192.168.33.10
User: vagrant
Password: vagrant


enjoy!!