# This was the vagrant file that I used. and It didn't work. The problem has been creating an internal network. Everything that I have tried has not worked.
# From my research it seam like this is the code that should work for sure. I have seen other ways to do it but this was the most common method people used.

# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|
	config.vm.provider :virtualbox do |v|
	  v.memory = 8096
	  v.cpus = 4
	  v.gui = true
  end

  config.vm.define "vm1" do |vm1|
	  vm1.vm.box = "StefanScherer/Windows_2019"
	  vm1.vm.hostname = "ADLab"
	  vm1.vm.network "private_network", type: "internal", ip: "192.168.33.10"
	end
end"

# The problem is the vm1.vm.network part. This is what is used to create an internal network. There is no reason to create a NAT network because it is done by default.
