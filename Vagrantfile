# -*- mode: ruby -*-
# vi: set ft=ruby :
$script = <<-SCRIPT
   if [[ $(/usr/bin/gcc 2>&1) =~ "no developer tools were found" ]] || [[ ! -x /usr/bin/gcc ]]; then
   touch /tmp/.com.apple.dt.CommandLineTools.installondemand.in-progress;
   PROD=$(softwareupdate -l |
     grep "\*.*Command Line" |
     head -n 1 | awk -F"*" '{print $2}' |
     sed -e 's/^ *//' |
     tr -d '\n')
   softwareupdate -i "$PROD" --verbose;
   fi

   if [[ ! -x /usr/local/bin/brew ]]; then
   ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)" </dev/null
   fi

   if [[ ! -x /usr/local/bin/ansible ]]; then
    echo "Info   | Install   | Ansible"
    brew update
    brew install ansible
   fi
   SCRIPT

Vagrant.configure("2") do |config|
 config.vm.box = "jhcook/macos-sierra"
 config.vm.network "private_network", ip: "192.168.33.10"
 config.vm.provider "virtualbox" do |vb|
  config.vm.synced_folder ".", "/vagrant", type: "rsync", group: "staff"
     

  config.vm.provision "shell", inline: $script, privileged: false
end
end

