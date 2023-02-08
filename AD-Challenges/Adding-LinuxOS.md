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

  - **sssd:** The System Security Services Daemon (SSSD) is a system service that provides access to various identity and authentication providers, including an Active Directory (AD) domain.
  - **realmd:** The Realmd service is used to discover and join identity domains such as Active Directory, and automate the configuration of required packages and services.
  - **oddjob:** The oddjob package provides a D-Bus service for running small, single-shot tasks for an unprivileged user, such as creating a home directory for a new user.
  - **oddjob-mkhomedir:** The oddjob-mkhomedir package is a script that creates a user's home directory if it does not already exist.
  - **adcli:** The adcli package provides a simple command-line interface to Active Directory domains. It can be used to join an Ubuntu machine to an AD domain, perform identity lookups, and change passwords.
  - **samba-common:** The Samba common package provides shared libraries and support files used by other Samba components, including the Samba client utilities.
  - **krb5-user:** The krb5-user package provides the user-space components required to use Kerberos authentication, which is a secure authentication system that is widely used for network authentication.
  - **sssd-krb5:** The sssd-krb5 package provides the SSSD back end for Kerberos authentication.

- By using the command ```realm discover``` we can see that ourdomain.com is not discoverable meaning we can not connect to it.
- To join we can use the command 
```
sudo realm join --user=a-radahn ourdomain.com -v
```
- The user needs someone who is authenticated to create a computer in the active directory. If we have everything correctly we should see the message ```* Successfully enrolled machine in realm```
- Using the command ```realm list``` we can see that we are connected.
- If we go back to our DC vm we can see that this vm is now a part of domain.         
![check](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-02-08%20155117.png)
- Now even if this vm is connected to our domain it still doesnt mean that we can log onto this with any other user in this domain.
