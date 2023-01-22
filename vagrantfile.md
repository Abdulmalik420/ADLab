# VagrantFile
- This was the vagrant file that I used. and It didn't work. The problem has been creating an internal network. Everything that I have tried has not worked.
- From my research it seam like this is the code that should work for sure. I have seen other ways to do it but this was the most common method people used.

```
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
end
```

- The problem is the vm1.vm.network part. This is what is used to create an internal network. There is no reason to create a NAT network because it is done by default.
- I kept getting an error that an internal network couldnt be created. And it also wasn't creating an internal network but a host-only network.
- I also tried this as well but this didn't work as well.
```
vm1.vm.network "private_network", :ip => "192.168.33.10", :adpater => 2
```

- This was one of the main errors that I have been getting regarting the network problem

```
Command: ["startvm", "6bb4a436-62c8-469f-bbfa-01b36751fd92", "--type", "headless"]

Stderr: VBoxManage.exe: error: Failed to open/create the internal network 'HostInterfaceNetworking-VirtualBox Host-Only Ethernet Adapter #2' (VERR_INTNET_FLT_IF_NOT_FOUND).
VBoxManage.exe: error: Failed to attach the network LUN (VERR_INTNET_FLT_IF_NOT_FOUND)
VBoxManage.exe: error: Details: code E_FAIL (0x80004005), component ConsoleWrap, interface IConsole
```
