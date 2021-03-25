# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "centos/7"

  config.vm.provider "virtualbox" do |v|
    v.memory = 256
    v.cpus = 1
  end

  config.vm.define "r1" do |r1|
    r1.vm.network "private_network", ip: "10.0.0.1", virtualbox__intnet: "link1"
    r1.vm.network "private_network", ip: "10.10.0.1", virtualbox__intnet: "link2"
    #management network
    r1.vm.network "private_network", ip: "10.10.10.11"
    r1.vm.hostname = "r1"
  end

  config.vm.define "r2" do |r2|
    r2.vm.network "private_network", ip: "10.0.0.2", virtualbox__intnet: "link1"
    r2.vm.network "private_network", ip: "10.20.0.2", virtualbox__intnet: "link3"
    #management network
    r2.vm.network "private_network", ip: "10.10.10.12"
    r2.vm.hostname = "r2"
  end

  config.vm.define "r3" do |r3|
    r3.vm.network "private_network", ip: "10.10.0.2", virtualbox__intnet: "link2"
    r3.vm.network "private_network", ip: "10.20.0.1", virtualbox__intnet: "link3"
    #management network
    r3.vm.network "private_network", ip: "10.10.10.13"
    r3.vm.hostname = "r3"
  end

  config.vm.provision "ospf", type:'ansible' do |ansible|
    ansible.inventory_path = './inventories/all.yml'
    ansible.playbook = './playbooks/ospf.yml'
  end
end
