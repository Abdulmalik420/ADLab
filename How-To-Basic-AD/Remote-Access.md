# Remote Connections
- In this how-to-basics we will be looking at how to remote connnect to computers and how we can log on to user as well.
### Remote Connect to Computer
- In order to connect to a computer in the domain we can use Remote Desktop Connection.
- Finally figured out this remote connection works. Not using Remote Desktop Connection but how it can be enabled using Group Policy. I will do another How to Basic for group policy but for this we will go little bit into using group policy to enable remote desktop connection.
### Remote Connect settings
- Inorder to be able to remote into a user computer the setting for it has to be enabled.
- When you go to this setting from a basic user account you will see that the setting can only be changed from an admin account.
- ![setting1](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-01-30%20102405.png)
- This is what you will see if you have nothing configured in group policy.
- But if you have remote connection configured in group policy this is what you will see.
- ![setting2](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-01-30%20102901.png)
- You can open up group policy management from here.
- ![openpolicy](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-01-30%20103824.png)
- You can either edit the general policy that would apply to the whole domain and over write any other policy or you can create a policy in the admin tab that applies to admins only.
- If its configured by using the general policy you would see this in the basic users remote settings "Some settings are managed by your organization". But if its configured in the policy of the admins you would see "this setting can be changed by admin".
- To create a new policy in the admin tab we can right click and create new policy
- ![create](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-01-30%20104827.png)
- Then you can right click the policy that you can edit the policy.
- Once you are in the editing screen you can see that there are two configurations one for computer and one for user. We want to configure the computer settings.
- You can follow these setsp. There are a lot of settings that can be configured. You can play around by seeing how changeing something effect others. But make sure that you know what you are changing and how you are changing it because if you mess something up you would need to know how you change it back.
- ![edit](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-01-30%20105834.png)
- In the Windows Component config you need to find the remote desktop services
- From here you can follow the remaining steps.
- ![edit2](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-01-30%20105920.png)
- Once your in the Connection folder the settings that you need to change is called "Allow users to connect remotely by using Remote Desktop Services". You can edit it by double clicking it or right click and edit. If you want to enable remote connect you would need to enable it.
- Once its enabled and saved you can close the editing windows.
- Now right click on the policy that you edited it and enforce it. Once thats done you can update it from the command prompt by using this code ```gpupdate/force```
- Now for the policy to be effected we need to restart the computer that we want to remote into. But before we do this we also want to be able to restart the computer remotely as well so we can restart teh computer anytime we cant from the DC computer.
- You can follw these settings.
- ![shutdown](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-01-30%20115114.png)
- We can then double click it and add the admin group to be able to force a shutdown.
- Then we can update the policy and restart the basic computer to have the policies to be effected.
- You should check the remote setting to make sure that the policy went into effect and that its enabled. Now you can remote connect into it.
- For some reason I cant get the remote shutdown to work. It should work with the command ```shutdown /r /m <ComputerName>``` but its not. I am going to look into it more to see what I am doing wrong.
### Remote Desktop Connect
- To use this remote connect that comes default in windows we need the name of the computer in the domain that we want to connect to.
![Connect](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-01-30%20140640.png)
- Then we can use our admin username and password to verify that we have access to remote connect into a computer thats in our domain. If you try to use a basic username and password it will say that this user doesnt havea access to remote connect into this computer.
- Once we give the admin user we can not controll this computer remotely.
- The blue bar at the top indicates that its connected                                                                          
![RemoteConnect](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-01-30%20140746.png)
- As you can see if another person is also logged in it will ask if you want to kick them out. You can also change this in group policy as well.
