# Challenge
- In this challenge I will be adding a vm that has a linux OS into the domain.
### Walk Through
- We need to create a vm like we did with the windows user that we had created. I will be using [ubuntu](https://ubuntu.com/download/desktop). Its the one with all the basic things that I might need.
- While creating the VM we need to add it to our internal network.
- Once we have the VM set up we can check that its connected to our internal network.
![ip](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-02-08%20151305.png)
- We can also check our active directory to make sure that a IP address was leased by our DHCP server.
- It can be checked by going to DHCP thats in the tool section.         
![dhcpcheck](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-02-08%20151609.png)
- We now need to add this VM to ourdomain.com
- For this to work we need to install some packages. And before we do we should update and upgrade our package manager which is "apt" in ubuntu.
```
sudo apt update
sudo apt upgrade
```
- Once we have it upgraded we can start installing the packages that we need.
```
sudo apt-get install sssd realmd oddjob oddjob-mkhomedir adcli samba-common krb5-user sssd-krb5
```
- While installing you will be prompted to put in a default domain that you want to connect to.
![prompt](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-02-08%20152852.png)
