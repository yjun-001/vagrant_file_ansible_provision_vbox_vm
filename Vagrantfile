# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "generic/ubuntu2004"
  config.vm.hostname = "hpc-node"
  config.vm.synced_folder '.', '/vagrant'
  # fix ubuntu ERROR: '~ansible' by install manually
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y ansible 
  SHELL

  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "provision.yaml"
  end
end
