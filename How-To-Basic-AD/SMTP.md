# SMTP (Simple Mail Transfer Protocol)
### Installing SMTP
- It can be installed the same way we have been doing other features as well.
- We can add feature and choose SMTP and install it.
![Settings](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-02-04%20163120.png)
### Configuring SMTP
- After it has been installed we can opne it from the tool tab.
- It isnt SMTP but IIS 6.0 Manager
- Once we open this we right click [SMTP Virtual Server #1] and open up its properties.
- There we can navigate over the the delivery tab and open outbound security                                                                    
![Setting2](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-02-04%20171720.png)
### Outbound Security
- Once you opne outbound security we can see these settings.
- Anonymous access: An account name or password is not required. This option disables authentication for the SMTP Server.
- Basic authentication: The account name and password of the server that you are connecting to are sent as clear text. Basic Authentication can be selected when sending e-mail to a personal account or an Exchange account. Because the credentials are passed in clear text, it is recommended to enable TLS encryption.
- Integrated Windows Authentication: The Windows domain account name and password are used to authenticate. The account you enter transmits the e-mails.
- TLS encryption: Similar to SSL, TLS secures the connection. Requires a valid SSL server certificate installed on this server.                                                                           
![Setting3](https://github.com/Abdulmalik420/ADLab/blob/main/ADLabPics/Screenshot%202023-02-04%20171757.png)
- What I did was creat another user that I would use for this and set up basic authentication.
