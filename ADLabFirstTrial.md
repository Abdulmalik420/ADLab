# ADLab First Trial
- At first I tried to do this lab by using vagrant and managing the the vm using that but it didn't workout.
- From the research that I have done it seams like it good to have two network adapters for the main machine. One a NAT so it can connect to the internet and another internal network for the other machines that are going to be managed by the AD of the main machine.
- Creating a vm in vagrant that uses both NAT and internal network either doesn't work or I was just not understaning how it can be done.

# ADLab Second Trial
- Since creating a vm using vagrant didnt work I tried creating a vm in virtual box it self and adding it to vagrant. Since vagrant takes .box file and virtual box creates vm using the file .vbox. 
- I converted the .vbox to .box and added it to vagrant but for some reason vagrant changed the vm settings and changed the internal network to host-only network again and it didnt work.
- I also tried creating a internal network using virtual box it self and it still said that no internal network of that name excites. 
- I thought just using internal network in virtualbox wasnt working so I created 2 different vm where one had a NAT and internal network and the other vm only had the internal network and the two vms could communicate with each other.
