# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define :web do |web_config|
    web_config.vm.box = "ubuntu/trusty64"
	web_config.vm.network :private_network, ip: "192.168.56.72", :adapter => 2
	web_config.vm.network "forwarded_port", guest: 80, host: 8888
	web_config.vm.provider "virtualbox" do |vb|
      vb.name = "box-web"
      vb.memory = 256
      vb.cpus = 1
    end
  end
  
  config.vm.define :db do |db_config|
    db_config.vm.box = "ubuntu/trusty64"
	db_config.vm.network :private_network, ip: "192.168.56.73", :adapter => 2
	db_config.vm.provider "virtualbox" do |vb|
      vb.name = "box-db"
      vb.memory = 512
      vb.cpus = 1
    end
  end
  
  config.vm.define :mgmt do |mgmt_config|
    mgmt_config.vm.box = "ubuntu/trusty64"
	mgmt_config.vm.network :private_network, ip: "192.168.56.71", :adapter => 2
	mgmt_config.vm.provider "virtualbox" do |vb|
      vb.name = "box-mgmt"
      vb.memory = 512
      vb.cpus = 1
      vb.gui = true
	  vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      vb.customize ["modifyvm", :id, "--ioapic", "on"]
    end
	mgmt_config.vm.provision "file", source: "ansible.cfg", destination: "~/ansible.cfg"
    mgmt_config.vm.provision "file", source: "hosts", destination: "~/hosts"
	mgmt_config.vm.provision "shell", inline: $configure
  end
  
end

$configure = <<SCRIPT
  sudo apt-get install -y software-properties-common
  sudo apt-add-repository ppa:ansible/ansible
  sudo apt-get update
  sudo apt-get install -y ansible
  ansible-playbook /vagrant/play-etc-hosts.yml -l local-box
  ansible-playbook /vagrant/play-ssh-keygen.yml -l mgmt-servers -e ansible_ssh_pass=vagrant
  ansible-playbook /vagrant/play-ssh-authorized-users.yml -e ansible_ssh_pass=vagrant
  ansible-playbook /vagrant/play-web.yml -l web-servers -e ansible_ssh_user=vagrant
  ansible-playbook /vagrant/play-git-clone.yml -l mgmt-servers -e ansible_ssh_user=vagrant
  ansible-playbook /home/vagrant/git/ansible-mysql-deploy-secure/play.yml -l db-servers -e ansible_ssh_user=vagrant
SCRIPT