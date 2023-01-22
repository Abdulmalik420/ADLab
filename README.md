# Requirements
- A Hybervisor (I used VirtualBox)
- A windows server. This is what I used [Windows Server 19](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2019)

# Walk-Through
### Set Up
- Create a VM using virtualbox. You can either use the ISO file or the VHD to set up the VM. The configurations depend on specs you want. But just be sure to set up two networks one NAT and the other an internal network. I like to name me internal nmetwork by celestial bodies so this one was names Moon.
- Once you open the VM it asks for you to "press Ctrl+Alt_Delete to unlock" but when you do using your keyvboard it effects your host and not the vm. A simple way to proceed is to use the soft keyboard option in virtualbox. It can be found by going to Input and then keyboard.
- Your can then set it up and login.
### Setting Up Network
- When you open your network settings (you can do this through the control panel) you should see two network
![Network start](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-01-22%20161202.png)

- You can tell which is which by seeing which one is connected to the internet which can only be the NAT.
![Network Mystery](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-01-22%20162036.png)

- Now that we have then figured out we can change their names to make it easier to identify
- Once that done we can configure an IP for the internal network
![Network Config](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-01-22%20163013.png)

