# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|
  config.vm.define "srv-attacker-out" do |srvattackerout|
    srvattackerout.vm.box = "centos/7"
    srvattackerout.vm.hostname = "srv-attacker-out"
    srvattackerout.vm.network "public_network", ip: "192.168.15.250" #Define IP estático
    srvattackerout.vm.provision "shell", path: "provision-attacker.sh"
      config.vm.provider "vmware_desktop" do |v|
        v.vmx["memsize"] = "512" #Define memoria
        v.vmx["numvcpus"] = "1"  #Define cpus
      end
  end
end

Vagrant.configure("2") do |config|
  config.vm.define "srv-attacker-in" do |srvattackerin|
    srvattackerin.vm.box = "centos/7"
    srvattackerin.vm.hostname = "srv-attacker-in"
    srvattackerin.vm.network "private_network", ip: "10.100.0.30" #Define IP estático
    srvattackerin.vm.provision "shell", path: "provision-attacker.sh"
      config.vm.provider "vmware_desktop" do |v|
        v.vmx["memsize"] = "512" #Define memoria
        v.vmx["numvcpus"] = "1"  #Define cpus
      end
  end
end

Vagrant.configure("2") do |config|
  config.vm.define "srv-target" do |srvtarget|
    srvtarget.vm.box = "centos/7"
    srvtarget.vm.hostname = "srv-target"
    srvtarget.vm.network "private_network", ip: "10.100.0.20" #Define IP estático
    srvtarget.vm.provision "shell", path: "provision-target.sh"
      config.vm.provider "vmware_desktop" do |v|
        v.vmx["memsize"] = "512" #Define memoria
        v.vmx["numvcpus"] = "1"  #Define cpus
      end
  end
end
