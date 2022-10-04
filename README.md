# vagrant_file_ansible_provision_vbox_vm

This repo is to create Open PBS VM node by using Vagrant & Ansible provision

### Prerequisite:
Reference this Repository to setup [local vagrant VM development environment](https://github.com/yjun-001/vagrant_vm_windows10)

### Vagrantfile to create VM ndoe:
```
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "generic/ubuntu2004"
  config.vm.hostname = "hpc-node"
  config.vm.synced_folder '.', '/vagrant'
  # fix ubuntu ERROR: '~ansible' by installing manually
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y ansible 
  SHELL

  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "provision.yaml"
  end
end
```
[Download Vagrantfile](https://raw.githubusercontent.com/yjun-001/vagrant_file_ansible_provision_vbox_vm/main/Vagrantfile)

### VM provisioning including:
  - install ansible
  - execute provision.yaml file
    - create pbsadmin user
    - create default password
    - setup sudo root access
    - reconfigure sshd_config and allow user to ssh into the VM with password
    - restart sshd deamon
