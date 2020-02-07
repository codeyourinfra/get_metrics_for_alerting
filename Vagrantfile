# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.define "monitor" do |monitor|
    monitor.vm.box = "codeyourinfra/monitor"
    monitor.vm.network "private_network", ip: "192.168.33.10"

    monitor.vm.provision "ansible" do |ansible|
      ansible.playbook = "monitoring-configuration.yml"
      ansible.inventory_path = "inventory.yml"
    end
  end

  (1..2).each do |i|
    config.vm.define "server#{i}" do |server|
      server.vm.box = "ubuntu/bionic64"
      server.vm.network "private_network", ip: "192.168.33.#{i+1}0"

      server.vm.provision "ansible" do |ansible|
        ansible.limit = "server#{i}"
        ansible.playbook = "servers-configuration.yml"
        ansible.inventory_path = "inventory.yml"
      end
    end
  end
end
