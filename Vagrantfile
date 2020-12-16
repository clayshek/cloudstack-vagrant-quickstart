# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # CloudStack Management Server VM
  config.vm.define "csmgmt", primary: true do |csmgmt|
    csmgmt.vm.box = "centos/7"
    csmgmt.vm.host_name = "csmgmt"
    csmgmt.vm.provider "hyperv" do |hyperv|
        hyperv.memory = "4096"
        hyperv.vmname = "csmgmt"
    end
  end

  # Hypervisor VMs 
  (1..2).each do |i|
    config.vm.define "kvm#{i}" do |kvm|
      kvm.vm.box = "centos/7"
      kvm.vm.host_name = "kvm#{i}.local"
      #kvm.vm.network "private_network", ip: "192.168.1.9#{i}", hostname: true
      kvm.vm.provider "hyperv" do |hyperv|
          hyperv.memory = "2048"
          hyperv.vmname = "kvm#{i}"
          hyperv.enable_virtualization_extensions = true
      end
    end  
  end

  config.vm.provision "file", source: "provisioning/", destination: "/home/vagrant/provisioning"
  config.vm.provision "ansible_local" do |ansible|
    ansible.provisioning_path = "/home/vagrant/provisioning"
    ansible.playbook = "playbook.yml"
    ansible.become = true  
    ansible.groups = {
      "cloudstack" => ["csmgmt"],
      "hypervisors" => ["kvm[1:2]"]
    }
  end

end