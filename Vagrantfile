# -*- mode: ruby -*-
# vi: set ft=ruby :

required_plugins = %w(vagrant-vbguest)
required_plugins.each do |plugin|
  system "vagrant plugin install #{plugin}" unless Vagrant.has_plugin? plugin
end

Vagrant.configure("2") do |config|

  config.vm.define "blockchain" do |d|
    d.vm.box = "centos/7"
    d.vm.box_version = "1809.01"
    d.vm.hostname = "blockchain"
    d.vm.network "private_network" , ip: "10.100.199.20"
    d.vm.synced_folder ".", "/vagrant", disabled: true
    d.vm.provision :shell, path: "scripts/passwordAuthentication.sh"
    d.vm.provision :shell, path: "scripts/provision.sh"
    d.vm.provider "virtualbox" do |v|
      v.memory = 5120
    end
  end

  if Vagrant.has_plugin?("vagrant-vbguest")
    config.vbguest.auto_update = false
    config.vbguest.no_remote = true
  end
end
