# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|
  config.vm.box = "monsenso/macos-10.13"
  config.vm.network "private_network", ip: "192.168.33.10"
  config.vm.provider "virtualbox" do |vb|
    config.vm.synced_folder ".", "/vagrant", type: "rsync", group: "staff"
    config.vm.provision "shell", path: "bootstrap.sh", privileged: false
    config.vm.provision "ansible_local" do |ansible|
      ansible.config_file = "ansible.cfg"
      ansible.inventory_path = "hosts"
      ansible.limit = "local"
      ansible.playbook = "local.yml"
      ansible.extra_vars = {
        "ansible_become_pass" => "vagrant"
      }
    end
  end
end
