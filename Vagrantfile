# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.require_version ">= 1.7.4"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box          = "windows_2016"
  config.vm.communicator = "winrm"

  ["vmware_fusion", "vmware_workstation"].each do |provider|
    config.vm.provider provider do |v, override|
      v.gui = true
      v.vmx["memsize"] = "8192"
      v.vmx["numvcpus"] = "2"
      v.vmx["vhv.enable"] = "TRUE"
      v.enable_vmrun_ip_lookup = false
    end
  end

  config.vm.provider "vmware_fusion" do |v|
    v.vmx["gui.fitguestusingnativedisplayresolution"] = "TRUE"
    v.vmx["mks.enable3d"] = "TRUE"
    v.vmx["mks.forceDiscreteGPU"] = "TRUE"
    v.vmx["gui.fullscreenatpoweron"] = "TRUE"
    v.vmx["gui.viewmodeatpoweron"] = "fullscreen"
    v.vmx["gui.lastPoweredViewMode"] = "fullscreen"
    v.vmx["sound.startconnected"] = "TRUE"
    v.vmx["sound.present"] = "TRUE"
    v.vmx["sound.autodetect"] = "TRUE"
  end

  config.vm.provider "virtualbox" do |v|
    v.gui = true
    v.customize ["modifyvm", :id, "--memory", 8092]
    v.customize ["modifyvm", :id, "--cpus", 2]
    v.customize ["modifyvm", :id, "--vram", 128]
    v.customize ["modifyvm", :id, "--clipboard", "bidirectional"]
    v.customize ["modifyvm", :id, "--accelerate3d", "on"]
    v.customize ["modifyvm", :id, "--accelerate2dvideo", "on"]
    v.linked_clone = true if Vagrant::VERSION =~ /^1.8/
  end

  config.vm.provider "hyperv" do |v|
    v.cpus = 2
    v.maxmemory = 4096
    v.differencing_disk = true
  end

  config.vm.provision "shell", path: "scripts/install-chocolatey.ps1", privileged: false
  config.vm.provision "shell", path: "scripts/install-git.ps1", privileged: false
  config.vm.provision "shell", path: "scripts/install-atom.ps1", privileged: false
  config.vm.provision "shell", path: "scripts/set-dns.ps1", privileged: false
  config.vm.provision "shell", path: "scripts/set-timezone.ps1", privileged: false
  config.vm.provision "shell", path: "scripts/set-keyboard.ps1", privileged: false
  config.vm.provision "shell", path: "scripts/insert-ssh-key.ps1", privileged: false
  config.vm.provision "shell", path: "scripts/install-posh-git.ps1", privileged: false
 
end
