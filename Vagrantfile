# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure('2') do |config|
  config.vm.box = "precise64-vmware"
  config.vm.box_url = "http://files.vagrantup.com/precise64_vmware_fusion.box"
  config.vm.hostname = "vodev-box-vmware"

  # This is to fix an issue with the postinstall.sh script
  # PostgreSQL was using LATIN1 instead of UTF-8 as a server_encoding value
  config.vm.provision :shell, :inline => "echo 'LC_ALL=\"en_US.UTF-8\"' > /etc/default/locale"
  # Chef >= 11.4.0 needs to be install. It requires ruby 1.9.3
  config.vm.provision :shell, :inline => "sudo aptitude update && sudo aptitude -y install build-essential && sudo aptitude -y install ruby1.9.3 && sudo gem install chef --version 11.6.0 --no-rdoc --no-ri --conservative"

  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = ["cookbooks", "cookbooks-src"]
    chef.roles_path = "roles"
    chef.add_role "vagrant-vodevbox"
  end
end