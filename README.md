# Requirements
- A Hybervisor (I used VirtualBox)
- A windows server. This is what I used [Windows Server 19](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2019)
- A regular windows which would be the basic users. This [Youtube Video](https://www.youtube.com/watch?v=5MU10eZbFeA) can help you with installing a iso file to use with virtualbox.
- If you would like another prespective on how this can be done you can check out [JonCyberGuy](https://github.com/JonCyberGuy/ActiveDirectoryLab).

# Walk-Through
### Set Up
- Create a VM using virtualbox. You can either use the ISO file or the VHD to set up the VM. The configurations depend on specs you want. But just be sure to set up two networks one NAT and the other an internal network. I like to name me internal nmetwork by celestial bodies so this one was names Moon.
- Once you open the VM it asks for you to "press Ctrl+Alt+Delete to unlock" but when you do using your keyvboard it effects your host and not the vm. A simple way to proceed is to use the soft keyboard option in virtualbox. It can be found by going to Input and then keyboard.
- Your can then set it up and login.
### Setting Up Network
- When you open your network settings (you can do this through the control panel) you should see two network
![Network start](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-01-22%20161202.png)

- You can tell which is which by seeing which one is connected to the internet which can only be the NAT.
![Network Mystery](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-01-22%20162036.png)

- Now that we have then figured out we can change their names to make it easier to identify
- Once that done we can configure an IP for the internal network
![Network Config](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-01-22%20163013.png)
- This was how I configured it. You can set the IP to anything and the subnet should be this. The DNS should be a loop back since this isnt connected to the internet so the DNS can be the build in DNS. The IP can be its own IP which is 172.16.0.1 or 127.0.0.1 is just a way to refure to back to it self.
- Now that we have the network part set up we can move on to the AD part.
### Active Directory Set Up
- To start of we need to open the server manager and this is where we can install active directory.
- We can install AD by pressing "add roles and features" which is one of the options in quick start.
- We can then press next untill be reach the Server Role section. Here we need to check the Active Directory Domain Services option. We can then proceed untill the install button is click able.
- Once its downloaded we can then make this server into a domain controller. The domain controller is one that controls everything that goes on in this server and they have access to everything.
### Domain Controller Set Up
- We need to promote this server into a domain controller. Since this is the only server it will give us a notice asking if we want to promte this server into a domain controller. The notice can be see up at the flag icon. We can then promote this server to a domain controller.
![Domain Notice](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-01-22%20172211.png)
- We can then name the domain.
![Domain Setup](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-01-23%20123653.png)
- After this we will be prompted to set up a password. Then we can continue until the install is click-able.
- Once its installed it be prompted to restart.
- Once it restarts we can see that our domain name is visiable next to our login name. And now we will be loging in a the domain controller.
- ![Domain End](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-01-23%20125121.png)
### Creating an Admin Account
- We will now be creating an admin account other then the adminstrator account that we hvae been using so far.
- In order to change user settings we need to open up the AD Users and Computers which can be found by going tool section up at the section tab.
- ![Admin Creation](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-01-23%20132253.png)
- The first thing that we want to do is to create a Organizational Unit (OU) which will be the place where we store all of the admin account.
- We can do that my right clicking on the our domain and creating a new OU.
![OU Creation](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-01-23%20133815.png)
- We can then name the OU that we are creating and uncheck the box that asks for deletion protection. Since this is a Lab in the case that we want to deleted we dont have go through the hassle of deleting when it has deletion protection.
- We can then proceed with creating a admin by making a new user in the admins OU.
![Admin Create](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-01-23%20134327.png)
- We can then fill in the info for the admin. And before we finish we should also check the never change password box as well. Since this is a Lab making it like this would just make it easier while we look through everything else.
![Admin Create](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-01-23%20135618.png)
- We will now give admin privileges to this user. We can do this by right clicking the user and going into their properties.
- We can then go into the member of section add this user to the domain admin folder.
![Admin Making](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-01-23%20140930.png)
- We can now log in as the admin by loging off the the adminstrator and changing user to the admin and logining on.
- Once we are loged in as the admin we can check our account by using this command which will give us a basic overview of the account.
```
net user <username>
```
- From this if we check the administrator account as well we can see the difference between the admin and administrator.
![User Comp](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-01-23%20142552.png)
- We can see that administrator has access to more groups and has more even to much power. While the admin only has access to the user and admin groups.
### Installing RAS/NAT
- What we are doing here is configuring a remote access service to give the computers that are connected to the internal network connection to the internet. So we are making the connection to NAT through remote access service.
- We can do this by adding a new feture like we added the active directory domain service.
- We can then select the remote access option to install in the server roles tab. In the role service tab we need to select the routing option and continue to install.
- Once it has installed we can configure it so that it does what it should.
### Configuring RAS/NAT
- To configure we need to go to the tool section and look for the routing and remote access option.
- We can then right click the PC name (local) and choose configure and follow the setup.
![Config](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-01-23%20155850.png)
- While seting up we need to choose the NAT option which is what we are trying to set up the RAS for.
![Config](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-01-23%20160043.png)
- We then need to choose the network that is our NAT network. Make sure that you are loged in as administrator and not admin. It seams like if you are loged in as admin you dont have access to the NAT network. We can then finish the configuration. Once finished the PC name(local) should now have a green arrow instead of a red arrow meaning that its working.
### DHCP Set UP
- Now that have the NAT connected via RAS we now need to configure a DHCP so that IP address can be assigned automaticly allowing the computers in the internal network to be able to connect to the internet.
- We can then install the DHCP server as we have done by pressing the adding roles and features in the quick start.
- In order to configure the DHCP we can do that through the tools section. 
![DHCP Config](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-01-23%20163526.png)
- For this server we are going to set up a IPv4 DHCP. By right clicking IPv4 we can creat a new scope which will be the range of the IP address that can be assigned.
- The range that I will be putting for the IP range will be 172.16.0.100-200 meaning that there will be 100 IPs that can be assigned at the same time.
- This is the range that I put.
![IP Range](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-01-23%20164000.png)
- Next we dont want any IP to be excluded so we can skip that part.
- We can also configure the lease time for the IP addressed. The leasing function of DHCP allow for IP addresses to be reused. This makes it so that one system would not be stuck with one IP. If they are not longer connecting to the network then leasing allows their IP to be assigned to someone else.
- The default gateway should be the IP address that you assigned to the internal network at the begining.
- Once the config is set up we can authorize the domain and refresh it and everything whould be up and running.
![Config](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-01-23%20165412.png)
### Checking Our Work
- What we want to do is to create a basic user. Just like how we did with the admin user just without the admin privileges. What I did since the user tab in the active directory is full of system users I created another OU called BASICUSERS.
- Now what we need to do is create a new vm using windows 10 iso that we had downloaded. But unlike the main machine we want to set the network to internal network that we made for the main machine.
- Dont be like me and download the home version of windows. It seams like the home version doesnt allow you to join a domain. Download the pro version that should work.
- When can then start up the vm and set it up.
- Once it has been set up what we need to do is to connect this vm to our domain that we had created. Mine was ourdomain.com.
- This can be done through the setting menu Rename this PC(Advanced). 
- Once we are there we can change the name of the PC and also add it to our domain. The login cred that is asked can either be the default administrator or the admin that we had created.
![Domain Join](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-01-24%20132117.png)
- Now that we have this PC in our domain. Once it restarts we can log in as the basic user that we had created.
![Basic User](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-01-24%20132606.png)
- Now that we have this PC connected to our domain we can see that in out AD the computer shows up.
![CheckPC](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-01-24%20132850.png)
### Bonus
- You can use a bash script to make the opening of both the DC and the user vm automaticly.
- Its a simple script that open the DC vm first and wait 1 min after open the user vm.
- Make sure that the file is sayed as .sh and you can make it so that its executable.
``` 
#! /bin/bash

start "E:\Devops\ADLab\ADLab.vbox"
sleep 60
start "E:\VMAD\WindowsUserAD\WindowsUserAD.vbox"
sleep 5
exit
```
