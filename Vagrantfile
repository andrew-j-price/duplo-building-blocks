# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.define :lb01 do |config|
    config.vm.box = "ubuntu/trusty64"
    config.vm.hostname = "lb01"
    config.vm.network :private_network, ip: "192.168.56.71", :adapter => 2
    config.vm.provider "virtualbox" do |vb|
      vb.memory = 256
      vb.cpus = 1
    end
  end

  config.vm.define :lb02 do |config|
    config.vm.box = "ubuntu/trusty64"
    config.vm.hostname = "lb02"
    config.vm.network :private_network, ip: "192.168.56.72", :adapter => 2
    config.vm.provider "virtualbox" do |vb|
      vb.memory = 256
      vb.cpus = 1
    end
  end

  config.vm.define :web01 do |config|
    config.vm.box = "ubuntu/trusty64"
    config.vm.hostname = "web01"
    config.vm.network :private_network, ip: "192.168.56.73", :adapter => 2
    config.vm.provider "virtualbox" do |vb|
      vb.memory = 256
      vb.cpus = 1
    end
  end

  config.vm.define :web02 do |config|
    config.vm.box = "ubuntu/trusty64"
    config.vm.hostname = "web02"
    config.vm.network :private_network, ip: "192.168.56.74", :adapter => 2
    config.vm.provider "virtualbox" do |vb|
      vb.memory = 256
      vb.cpus = 1
    end
  end
  
  config.vm.define :db01 do |config|
    config.vm.box = "ubuntu/trusty64"
    config.vm.hostname = "db01"
    config.vm.network :private_network, ip: "192.168.56.76", :adapter => 2
    config.vm.provider "virtualbox" do |vb|
      vb.memory = 256
      vb.cpus = 1
    end
  end

  config.vm.define :sa01 do |config|
    config.vm.box = "ubuntu/trusty64"
    config.vm.hostname = "sa01"
    config.vm.network :private_network, ip: "192.168.56.80", :adapter => 2
    config.vm.provider "virtualbox" do |vb|
      vb.memory = 256
      vb.cpus = 1
    end
  end

  config.vm.define :duplo do |config|
    config.vm.box = "ubuntu/trusty64"
    config.vm.hostname = "duplo"
    config.vm.network :private_network, ip: "192.168.56.79", :adapter => 2
    config.vm.provider "virtualbox" do |vb|
      vb.memory = 192
      vb.cpus = 1
      vb.gui = false
      vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      vb.customize ["modifyvm", :id, "--ioapic", "on"]
    end
    config.vm.provision "file", source: "ansible_control_files/ansible.cfg", destination: "~/ansible.cfg"
    config.vm.provision "file", source: "ansible_control_files/hosts", destination: "~/hosts"
    config.vm.provision "shell", inline: $configure
  end
  
end

$configure = <<SCRIPT
  sudo apt-get install -y software-properties-common
  sudo apt-add-repository ppa:ansible/ansible
  sudo apt-get update
  sudo apt-get install -y ansible
  ansible-playbook /vagrant/playbooks/play-etc-hosts.yml -l local
  ansible-playbook /vagrant/playbooks/play-etc-hosts.yml
  ansible-playbook /vagrant/playbooks/play-ssh-keygen.yml -l local
  ansible-playbook /vagrant/playbooks/play-ssh-authorized-users.yml
  ansible-playbook /vagrant/playbooks/play-load-balancer.yml
  ansible-playbook /vagrant/playbooks/play-web-server.yml
  ansible-playbook /vagrant/playbooks/play-database-server.yml
  ansible-playbook /vagrant/playbooks/play-service-assurance-client.yml
  ansible-playbook /vagrant/playbooks/play-service-assurance-server.yml
SCRIPT
