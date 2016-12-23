# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.require_version ">= 1.6.0"
VAGRANTFILE_API_VERSION = "2"

require 'yaml'
servers = YAML.load_file(File.join(File.dirname(__FILE__), 'vagrant-instances.yml'))

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  servers.each do |servers|
    config.vm.define servers["name"] do |srv|
      srv.vm.box = servers["box"]
      srv.vm.hostname = servers["name"]
      srv.vm.network "private_network", ip: servers["ip"], :adapter => 2
      srv.vm.provider :virtualbox do |vb|
        vb.memory = servers["ram"]
        vb.cpus = servers["cpus"]
      end
      srv.vm.provision "shell", inline: $keys
    end
  end
  config.vm.define :duplo do |config|
    config.vm.box = "ubuntu/trusty64"
    config.vm.hostname = "duplo"
    config.vm.network :private_network, ip: "192.168.56.79", :adapter => 2
    config.vm.provider "virtualbox" do |vb|
      vb.memory = 384
      vb.cpus = 1
      vb.gui = false
      vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      vb.customize ["modifyvm", :id, "--ioapic", "on"]
    end
    config.vm.provision "shell", inline: $keys
    config.vm.provision "shell", inline: $deploy
  end
end

$keys = <<SCRIPT
  sudo cp /vagrant/authorized_keys /root/.ssh/authorized_keys
  cat /vagrant/authorized_keys >> /home/vagrant/.ssh/authorized_keys
SCRIPT

$deploy = <<SCRIPT
  sudo apt-get install -y software-properties-common
  sudo apt-add-repository ppa:ansible/ansible
  sudo apt-get update
  sudo apt-get install -y ansible
  cd /vagrant/
  ansible-playbook deploy.yml
SCRIPT
