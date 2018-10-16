# Personal computer configuration.

This is the idalab MacBook configuration. We use this process to set up our work machines for development, now you can use it too.

### Acknowledgements

None of this would exist without Noa Shinitski (https://github.com/noashin) and Daniel Kirsch (https://github.com/kirel)

### Set up

Clone the repository to your computer, copy and pasting its link (above):

    $ git clone COPY_PASTED_LINK

Run the bootstrap script. This will ensure gcc,
[Homebrew](http://brew.sh/), and [Ansible](http://docs.ansible.com/) are
installed:

    $ cd macbook-configuration/
    $ ./bootstrap.sh
    $ ansible-playbook local.yml -K -i hosts

The `-K` flag means that Ansible will prompt you for your sudo password
before it executes the playbook.

If it's your first time, go brew some coffee or tea because this will take a while.


### How it works

The starting point is the file 'local.yml' in the root of this repository. There you can find which roles will be included in the run, as well as some parameters for the execution of the pyenv role. The folder roles contains one folder for each role that is listed in local.yml, which in turn contains a folder 'tasks' where you will find a file called 'main.yml'. This file contains the specific install instructions for the role.
To clarify using a short example: The role 'common' in local.yml is meant to refer to usual desktop apps that are needed to our jobs. So if you look inside the folder roles -> common -> tasks you will find the main.yml that specifies exactly which programs will be installed if the role common is included in the local.yml at the root of the repository.

After you start ansible-playbook it will install all roles defined in local.yml according to each roles specific main.yml file.


### Testing and development - Using Vagrant to configure and run a virtual machine:

You only need to read this if you want to test and/or develop this process in a virtual machine.

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
