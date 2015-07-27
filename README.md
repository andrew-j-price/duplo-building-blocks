# vagrant-ansible-building-blocks

Purpose of this project to show the building blocks for automating a multi VM Vagrant environment managed and configured via Ansible with a simple "vagrant up"

Tha management node is created as a VM so Windows users can run it, as well as it is better suited for testing and illustration.

Vagrant and Ansible are basically self-documenting, but the project will:
* Create 3 VMs (mgmt, web, and db)
* Auto configure Ansible
* Populate the /etc/hosts file
* Create a SSH key
* Copy that SSH public key to authorized_keys
* Deploy some packages on a web server
* Clone an additional project on github
* Using the cloned project, deploy and secure MySQL
