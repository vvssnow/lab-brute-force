# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|
  config.vm.define "srvcentosattacker" do |srvcentosattacker|
    srvcentosattacker.vm.box = "centos/7"
    srvcentosattacker.vm.hostname = "srv-attacker"
    srvcentosattacker.vm.network "public_network", ip: "192.168.15.220" #"Best pratics define static ip here[You decision]"
    srvcentosattacker.vm.provision "shell", path: "provision-attacker.sh"
      config.vm.provider "vmware_desktop" do |v|
        v.vmx["ethernet0.pcislotnumber"] = "32"
        v.vmx["memsize"] = "512"
        v.vmx["numvcpus"] = "1"
      end
  end
end

Vagrant.configure("2") do |config|
  config.vm.define "srvcentostarget" do |srvcentostarget|
    srvcentostarget.vm.box = "centos/7"
    srvcentostarget.vm.hostname = "srv-target"
    srvcentostarget.vm.network "public_network", ip: "192.168.15.240" #"Best pratics define static ip here [You decision]"
    srvcentostarget.vm.provision "shell", path: "provision-target.sh"
      config.vm.provider "vmware_desktop" do |v|
        v.vmx["ethernet0.pcislotnumber"] = "32"
        v.vmx["memsize"] = "512"
        v.vmx["numvcpus"] = "1"
      end
  end
end