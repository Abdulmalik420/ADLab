# ADLab First Trial
- At first I tried to do this lab by using vagrant and managing the the vm using that but it didn't workout.
- From the research that I have done it seams like it good to have two network adapters for the main machine. One a NAT so it can connect to the internet and another internal network for the other machines that are going to be managed by the AD of the main machine.
- Creating a vm in vagrant that uses both NAT and internal network either doesn't work or I was just not understaning how it can be done.
## VagrantFile
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
	  vm1.vm.communicator = "winrm"
	  vm1.winrm.port = 55985
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

Stderr: VBoxManage.exe: error: Failed to open/create the internal network 
'HostInterfaceNetworking-VirtualBox Host-Only Ethernet Adapter #2' (VERR_INTNET_FLT_IF_NOT_FOUND).
VBoxManage.exe: error: Failed to attach the network LUN (VERR_INTNET_FLT_IF_NOT_FOUND)
VBoxManage.exe: error: Details: code E_FAIL (0x80004005), component ConsoleWrap, interface IConsole
```

# ADLab Second Trial
- Since creating a vm using vagrant didnt work I tried creating a vm in virtual box it self and adding it to vagrant. Since vagrant takes .box file and virtual box creates vm using the file .vbox. 
- I converted the .vbox to .box and added it to vagrant but for some reason vagrant changed the vm settings and changed the internal network to host-only network again and it didnt work.
- I also tried creating a internal network using virtual box it self and it still said that no internal network of that name excites. 
- I thought just using internal network in virtualbox wasnt working so I created 2 different vm where one had a NAT and internal network and the other vm only had the internal network and the two vms could communicate with each other.
## VagrantFile
- This was the vagrant file that I used for the second trial
```
# -*- mode: ruby -*-
# vi: set ft=runy :
Vagrant.configure("2") do |config|
  config.vm.box = "ADLab"
  config.vm.communicator = "winrm"
  config.winrm.port = 55985
end
```
    
