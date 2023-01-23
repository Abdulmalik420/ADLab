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
