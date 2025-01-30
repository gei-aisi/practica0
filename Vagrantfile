# -*- mode: ruby -*-
# vi: set ft=ruby :
require_relative 'provisioning/vbox.rb'
VBoxUtils.check_version('7.1.6')
Vagrant.require_version ">= 2.4.3"

Vagrant.configure("2") do |config|
    # Box and hostname settings
    config.vm.box = "XXX"
    config.vm.box_version = "XXX"
    config.vm.box_check_update = XXX
    config.vm.hostname = "XXX" # You MUST use your prefix here

    # Network and port forwarding settings
    config.vm.network "XXX", guest: XXX, host: XXX
    config.vm.network "XXX", type: "XXX"
    config.vm.network "XXX", ip: "XXX", netmask: "XXX"

    # Synced folder
    config.vm.synced_folder "XXX", "XXX", mount_options: ["dmode=XXX,fmode=XXX"]

    # Configure vbguest and hostmanager plugins
    config.vbguest.auto_update = false
    config.hostmanager.enabled = XXX
    config.hostmanager.manage_host = XXX
    config.hostmanager.manage_guest = XXX

    # Provider-specific customizations (CPU, memory, disk...)
    config.vm.provider "virtualbox" do |vb|
	vb.name = "AISI-P0-#{config.vm.hostname}"
	vb.gui = false
	vb.cpus = XXX
	vb.memory = XXX

	sasController = "SAS Controller"
	diskFile = "VMdisk-SAS.vmdk"
	
	# Create the virtual disk if doesn't exist
	unless File.exist?(diskFile)
		vb.customize ["createmedium", "XXX", "--filename", XXX, "--format", "XXX", "--size", XXX]
	end

	# Add storage SAS controller only when the VM is provisioned for the first time
	unless File.exist?(".vagrant/machines/default/virtualbox/action_provision")
		vb.customize ["storagectl", :id, "--name", sasController, "--add", "XXX", "--portcount", XXX]
	end

	# Attach the virtual disk into the storage SAS controller
	vb.customize ["storageattach", :id, "--storagectl", sasController, "--port", XXX, "--device", 0, "--type", "XXX", "--medium", XXX]
    end

    # Embedded provisioning through shell script
    config.vm.provision "shell", run: "XXX", inline: <<-SHELL
	apt update
	# Complete the following commands
	apt install -y
	systemctl
	systemctl
	mkfs.ext4
	mkdir -p
    SHELL
    
    # Provisioning through an external shell script
    config.vm.provision "shell", run: "XXX", path: "provisioning/script.sh", args: "XXX"
end
