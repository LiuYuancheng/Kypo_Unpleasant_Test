# Generated by Cyber Sandbox Creator 3.1.0
# https://gitlab.ics.muni.cz/muni-kypo-csc/cyber-sandbox-creator
#
# -*- mode: ruby -*-
# vi: set ft=ruby :

ansible_groups = {
  "hosts" => ["attacker", "web-server"], 
  "routers" => ["router"], 
  "ssh" => ["router", "attacker", "web-server"], 
  "winrm" => [], 
  "ansible" => ["router", "attacker", "web-server"], 
  "user-accessible" => ["attacker"]
}

Vagrant.configure("2") do |config|

  # Device(router): router
  config.vm.define "router" do |device|
    device.vm.hostname = "router"
    device.vm.box = "munikypo/debian-10"
    device.vm.provider "virtualbox" do |vb|
      vb.memory = 1024
      vb.cpus = 1
    end
    device.vm.synced_folder ".",
      "/vagrant",
      type: "rsync",
      rsync__exclude: ".git/"
    device.vm.network "private_network",
      virtualbox__intnet: "switch",
      ip: "10.32.51.1",
      netmask: "255.255.255.0"
    device.vm.network "private_network",
      virtualbox__intnet: "internet-connection",
      ip: "100.100.100.1",
      netmask: "255.255.255.0"
    device.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "preconfig/playbook.yml"
      ansible.groups = ansible_groups
      ansible.limit = "router"
    end
    device.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "provisioning/playbook.yml"
      ansible.groups = ansible_groups
      ansible.limit = "router"
    end
  end

  # Device(host): web-server
  config.vm.define "web-server" do |device|
    device.vm.hostname = "web-server"
    device.vm.box = "munikypo/debian-10"
    device.vm.provider "virtualbox" do |vb|
      vb.memory = 1024
      vb.cpus = 1
    end
    device.vm.synced_folder ".",
      "/vagrant",
      type: "rsync",
      rsync__exclude: ".git/"
    device.vm.network "private_network",
      virtualbox__intnet: "switch",
      ip: "10.32.51.173",
      netmask: "255.255.255.0"
    device.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "preconfig/playbook.yml"
      ansible.groups = ansible_groups
      ansible.limit = "web-server"
    end
    device.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "provisioning/playbook.yml"
      ansible.groups = ansible_groups
      ansible.limit = "web-server"
    end
  end

  # Device(host): attacker
  config.vm.define "attacker" do |device|
    device.vm.hostname = "attacker"
    device.vm.box = "munikypo/kali-2020.4"
    device.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus = 1
    end
    device.vm.synced_folder ".",
      "/vagrant",
      type: "rsync",
      rsync__exclude: ".git/"
    device.vm.network "private_network",
      virtualbox__intnet: "switch",
      ip: "10.32.51.12",
      netmask: "255.255.255.0"
    device.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "preconfig/playbook.yml"
      ansible.groups = ansible_groups
      ansible.limit = "attacker"
    end
    device.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "provisioning/playbook.yml"
      ansible.groups = ansible_groups
      ansible.limit = "attacker"
    end
  end
end
