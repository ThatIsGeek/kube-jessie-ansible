# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "debian/jessie64"

  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "/vagrant/playbook.yml"
    ansible.install = true
  end

  config.vm.define "k8s-master" do |config|
    config.vm.hostname = "k8s-master"
    config.vm.network :private_network, ip: "10.0.0.3"
    config.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "/vagrant/playbook.yml"
      ansible.groups = ['master']
    end
  end

  config.vm.define "k8s-node-1" do |config|
    config.vm.hostname = "k8s-node-1"
    config.vm.network :private_network, ip: "10.0.0.4"
    config.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "/vagrant/playbook.yml"
      ansible.groups = ['minion']
    end
  end

  config.vm.provider "virtualbox"
end
