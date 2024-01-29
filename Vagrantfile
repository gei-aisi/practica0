# -*- mode: ruby -*-
# vi: set ft=ruby :
require_relative 'provisioning/vbox.rb'
VBoxUtils.check_version('7.0.14')
Vagrant.require_version ">= 2.4.1"

Vagrant.configure("2") do |config|
    # Box and hostname settings
    config.vm.box = "XXX"
    config.vm.box_version = "XXX"
    config.vm.box_check_update = XXX
    config.vm.hostname = "xxx2324"

    # Network and port forwarding settings
    config.vm.network "XXX", guest: XXX, host: XXX
    config.vm.network "XXX", type: "XXX"
    config.vm.network "XXX", ip: "XXX", netmask: "XXX"

    # Synced folder
    config.vm.synced_folder "XXX", "XXX", mount_options: ["dmode=XXX,fmode=XXX"]

    # Configure hostmanager and vbguest plugins
    config.hostmanager.enabled = XXX
    config.hostmanager.manage_host = XXX
    config.hostmanager.manage_guest = XXX
    config.vbguest.auto_update = false

    # Provider-specific customizations (CPU, memory, disk...)
    config.vm.provider "virtualbox" do |vb|
	vb.name = "AISI-P0-#{config.vm.hostname}"
	vb.gui = false
	vb.cpus = XXX
	vb.memory = XXX

	sasController = "SAS Controller"
	disk = "diskVM-SAS.vmdk"
	
	# Create the virtual disk if doesn't exist
	unless File.exist?(disk)
		vb.customize ["createmedium", "XXX", "--filename", disk, "--format", "XXX", "--size", XXX]
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
	mkdir
    SHELL
    
    # Provisioning through an external shell script
    config.vm.provision "shell", run: "XXX", path: "provisioning/script.sh", args: "xxx2324"
end
