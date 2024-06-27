<h1>Active Directory Home Lab - Adding Users with PowerShell</h1>

<h2>Description</h2>
This Active Directory home lab aims to design, implement, and secure an Active Directory environment using Windows Server 2019 and VirtualBox for virtualization. The project involves setting up a Domain Controller (DC) with dual NICs for outside internet and internal network communication, configuring DHCP and RAS/NAT services, and deploying a Windows 10 client machine for testing. A PowerShell script will automate the creation of over 1,000 user accounts, removing the need to input users manually. Lastly, the user accounts are tested to verify successful configuration.

<h2>Key Objectives</h2>

- <b>Design and Implement Active Directory Environment in Server 2019</b>
- <b>Configure Domain Controller and Network Services - DHCP, RAS, NAT</b>
- <b>Automate User Creation with PowerShell</b>
- <b>Deploy Windows 10 Client Machine and Validate</b>

<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b> 

<h2>Environments Used </h2>

- <b>Oracle VirtualBox</b>
- <b>Windows 10 VM (Client Machine)</b>
- <b>Windows Server 2019 (DC)</b>

<h2>Project Diagram:</h2>
<br />
<img src="https://imgur.com/i0NQs4X.png"height="80%" width="80%"/>
<br />

<h2>Domain Controller Configuration:</h2>

<p align="center">
<br />
Creating the Windows Server 2019 machine. Making sure to set up the two NICs for the internet and internal network.
<br />
<br />
<img src="https://imgur.com/E5DNCwi.png" height="80%" width="80%"/>
<br />
<br />
<img src="https://imgur.com/i7ZgI2Z.png"height="80%" width="80%"/>
<br />
<br />
Renaming the device to simplify things.
<br/>
<br/>
<img src="https://imgur.com/6uccNNQ.png" height="80%" width="80%"/>
<br />
<br />
Here we see our two network adaptors. Now we need to verify which is for the internet and which is for the internal network, name them appropriately, and configure the proper IP address for the internal network.
<br />
<br />
<img src="https://imgur.com/0Pmiaw3.png"height="80%" width="80%"/>
<br />
<br />
First, we can check the details of the Ethernet network and look at the IP address. We see it is 10.0.2.15, which would be our home network IP address for NAT. After identifying that, we can go ahead and rename the network to better identify it.
<br/>
<br/>
<img src="https://imgur.com/zyJwDtt.png" height="80%" width="80%"/>
<br />
<br />
Next, we can take a look at the IP address of Ethernet 2, which is 169.254.169.131. This means that this adapter was searching for a DHCP server to get an IP address from somewhere, but was unable to find one. So it had an IP address automatically assigned to it by the virtual machine, letting us know that this is the internal network. 
<br />
<br />
After understanding that, we can go ahead an also rename this network.
<br /> 
<br />
<img src="https://imgur.com/qaUGVpp.png" height="80%" width="80%"/>
<br /> 
<br />
Now that we know which network is which, we can go ahead and assign the proper IP address to the internal network according to our diagram. 
<br />
<br />
We won't designate a default gateway because the DC will serve as the gateway since it has two NICs. 
<br />
<br />
We'll also designate a /24 subnet mask and use our loopback address for the preferred DNS server.
<br />
<br />
<img src="https://imgur.com/gF2n0vB.png" height="80%" width="80%"/>
<br />
<br />
<img src="https://imgur.com/FvevBJ4.png" height="80%" width="80%"/>
<br /> 
<br />
Next, we will install AD DS and create a domain
<br/>
<br/>
<img src="https://imgur.com/FWJyL58.png" height="80%" width="80%"/>
<br/>
<br/>
AD DS installation complete:
<br/>
<br/>
<img src="https://imgur.com/j6agXlE.png" height="80%" width="80%"/>
<br/>
<br/>
Promoting the server to a DC:
<br/>
<br/>
<img src="https://imgur.com/vRPW6qO.png" height="80%" width="80%"/>
<br/>
<br/>
After promoting the server to a DC, we are now able to log in to the domain with the built-in admin account.
<br/>
<br/>
<img src="https://imgur.com/M3hEunZ.png" height="80%" width="80%"/>
<br/>
<br/>
Now we'll create a dedicated admin account instead of using the built in admin account.
<br/>
<br/>
To do this, we'll create an organizational unit (OU) to put the admin account in.
<br/>
<br/>
I named the OU, _ADMINS
<br/>
<br/>  
<img src="https://imgur.com/Ktxo1LE.png" height="80%" width="80%"/>
<br/>
<br/>
Inside the OU, we've created the user, Anthony Bastone.
<br/>
<br/>
<img src="https://imgur.com/vPbdM5j.png" height="80%" width="80%"/>
<br/>
<br/>
<img src="https://imgur.com/wXcXnRy.png" height="80%" width="80%"/>
<br/>
<br/>
Since we've now created the user, we need to make them an domain admin.
<br/>
<br/>
This can be done by right clicking on the user, selecting properties, member of, and then add. Enter the object name, then press OK.
<br/>
<br/>
<img src="https://imgur.com/LfwGI6t.png" height="80%" width="80%"/>
<br/>
<br/>
Let's verify that we can login to the domain admin account now.
<br/>
<br/> 
<img src="https://imgur.com/r2uxnXn.png" height="80%" width="80%"/> 
<br/>
<br/>
Once we've logged into the domain admin account, we'll go back to the Server Manager and add roles and features. We will install remote access and routing.
<br/>
<br/>
<img src="https://imgur.com/laoz7CO.png" height="80%" width="80%"/>
<br/>
<br/>
<img src="https://imgur.com/WtFoaAD.png" height="80%" width="80%"/>
<br/>
<br/>
Select our destination server: 
<br/>
<br/> 
<img src="https://imgur.com/qv18iDg.png" height="80%" width="80%"/>
<br/>
<br/>
Installation succeeded:
<br/>
<br/>
<img src="https://imgur.com/qqOZJic.png" height="80%" width="80%"/>
<br/>
<br/>
Next, we'll go to routing and remote access tools to configure and enable our NAT internet connection.
<br/>
<br/>
<img src="https://imgur.com/0xUSUdJ.png" height="80%" width="80%"/>
<br/>
<br/> 
<img src="https://imgur.com/PhAadmh.png" height="80%" width="80%"/>
<br/>
<br/> 
<img src="https://imgur.com/W840Che.png" height="80%" width="80%"/>
<br/>
<br/>
We want to make sure to select our X_INTERNET_X interface to connect to the internet.
<br/>
<br/>
<img src="https://imgur.com/NbPcSuX.png" height="80%" width="80%"/>
<br/>
<br/>  
Once RAS/NAT has been configured, we will set up a DHCP server on the DC to allow the Windows 10 clients to get an IP address and be able to browse the internet.
<br/>
<br/>  
<img src="https://imgur.com/tHfV3KV.png" height="80%" width="80%"/>
<br/>
<br/>
DHCP installation succeeded:
<br/> 
<br/>
<img src="https://imgur.com/U00JLtl.png" height="80%" width="80%"/>
<br/>  
<br/>
Just like routing and remote access tools, we'll select DHCP tools to set up our scope.
<br/> 
<br/>
There will be no IP exlusions and the lease duration isn't too important here since this is a lab, so we'll leave it at the default of 8 days.
<br/> 
<br/>
<img src="https://imgur.com/Bo0jT6K.png" height="80%" width="80%"/>
<br/>  
<br/>
<img src="https://imgur.com/CARctRc.png" height="80%" width="80%"/>
<br/>
<br/> 
<img src="https://imgur.com/nF2A8yC.png" height="80%" width="80%"/>
<br/>
<br/>
Adding the IP address for the router that will be used by the clients. The clients will be using the internal NIC as the default gateway/router.
<br/>
<br/>
<img src="https://imgur.com/TIs6pfL.png" height="80%" width="80%"/>
<br/> 
<br/>
<img src="https://imgur.com/dLxmOrG.png" height="80%" width="80%"/>
<br/>
<br/>
Authorized and refreshed by right clicking on the domain. We now see the green check marks next to IPv4 and IPv6 letting us know we're good.
<br/>
<br/>
<img src="https://imgur.com/EAFli4Y.png" height="80%" width="80%"/>
<br/> 
<br/>
Noticed that the our router did not populate in the IPv4 Sever Options folder. To fix that, we just add it in
<br/>  
<br/>
<img src="https://imgur.com/MvMCPsV.png" height="80%" width="80%"/>
<br/>
<br/> 
Now that we've configured out router and DHCP scope, we can get our PowerShell script.
<br/>
<br/>
We'll download the PowerShell script by Josh Madakor. This will allow us to create over 1,000 users without having to do it manually.
<br/>
<br/>
<img src="https://imgur.com/leYSQzI.png" height="80%" width="80%"/>
<br/>
<br/>
Extract the script onto the desktop and then open the "names" text file.
<br/> 
<br/>
<img src="https://imgur.com/df8JTok.png" height="80%" width="80%"/>
<br/>  
<br/>
Added my own name to make it easier to remember when testing on the client machine.
<br/>  
<br/>
<img src="https://imgur.com/IWZf2zk.png" height="80%" width="80%"/>
<br/>
<br/>
Now we'll run PowerShell ISE as an administrator and open the PowerShell script.
<br />
<br />
<img src="https://imgur.com/24vdS6l.png" height="80%" width="80%"/>
<br />
<br />
Before we can run the script, we need to set the execution policy to unrestricted and change directories to where the script is at with the following commands:
<br />
<br />
Set-ExecutionPolicy unrestricted
<br /> 
<br />
cd C:\users\a-abastone\Desktop\AD_PS-master
<br /> 
<br />
We can then list the contents of the directory and see that our file is indeed located there.
<br /> 
<br />
<img src="https://imgur.com/chQKAFr.png" height="80%" width="80%"/>
<br /> 
<br />
When looking at the script that we've opened, we can see that we will be:
<br />
<br />
- Creating a password for all users.
<br />
<br />
- Pulling the names file for PowerShell to run.
<br />
<br />
- Converting the plain text password into a secure string for PowerShell to run.
<br />
<br />
- Creating a new organization unit (OU) named _USERS, and are not protecting it from accidental deletion in case we want to practice this lab again.
<br />
<br />
- Running a loop to run the following block of code that will create and enable the users themselves with the names file.
<br />
<br />
<img src="https://imgur.com/d6hZzRI.png" height="80%" width="80%"/>
<br />
<br />
Now we'll go ahead and run the script.
<br />
<br />
<img src="https://imgur.com/JbkCGMc.png" height="80%" width="80%"/>
<br />
<br />
Now the users have been created. We can go into Active Directory and see that the _USERS file has been created. Inside the file we'll find all of the users that have been created as well.
<br />
<br />
<img src="https://imgur.com/1ZtgcuI.png" height="80%" width="80%"/>
<br />
<br />
To dig even deeper, we can right click on the file and select find to search for a specific user.
<br />
<br />
<img src="https://imgur.com/EKCQ3nc.png" height="80%" width="80%"/>
<br /> 
<br />
We can also switch out of the _USERS file, into the domain, and search again. We notice that we've now found the user and the administrator account.
<br />
<br />
<img src="https://imgur.com/UlOSgYg.png" height="80%" width="80%"/>
<br />
<br /> 
<br />
<br />
<br />
  
<h2>Windows 10 VM (Client Machine):</h2>

<p align="center">
  
<br />
Now that we've successfully created over 1,000 users with PowerShell, we can go ahead and configure our Windows 10 client machine on the internal NIC to test our work.
<br />
Connecting this VM to the internal network will allow us to get a DHCP address from the DC.
<br />
<br />
<img src="https://imgur.com/dyN5MDU.png" height="80%" width="80%"/>
<br />
<br />
Opened up the command line and ran the following command, ipconfig, to verify that we are indeed connected to the internet with the proper IP address and default gateway:
<br />
<br />
<img src="https://imgur.com/9xsPPQr.png" height="80%" width="80%"/>
<br />
<br />
We'll also go ahead and ping google.com as well as our own DC, bastonesdomain.com, to test for connectivity.
<br />
<br />
<img src="https://imgur.com/ktE2cQ2.png" height="80%" width="80%"/>
<br />
<br />
After verifying connectivity, let's now rename the device and join the device to the domain via our created admin account.
<br />
<br />
To do this, we will go to the settings and Rename this PC (advanced), instead of the regular Rename this PC.
<br />
<br />
<img src="https://imgur.com/ENytD3g.png" height="80%" width="80%"/>
<br />
<br />
<img src="https://imgur.com/TVH3jFT.png" height="80%" width="80%"/>
<br /> 
<br />
<img src="https://imgur.com/P3xEJVS.png" height="80%" width="80%"/>
<br />
<br />
<img src="https://imgur.com/IRYJAlu.png" height="80%" width="80%"/>
<br />
<br />
<br />
<br />
<br />
<h2>Verify Successful Configuration:</h2>

<p align="center">
  
<br />
We've now joined the client machine to our DC, so we'll go back to the DC and open up our DHCP to verify that everything has been configured properly.
<br />
<br />
We can see our lease from our client machine in the scope that we've created.
<img src="https://imgur.com/igjqc0R.png" height="80%" width="80%"/>
<br />
<br />
Within Active Directory, we can go into the computers file and see that our client machine is now a member of the domain.
<br />
<br />
<img src="https://imgur.com/N47hqgX.png" height="80%" width="80%"/>
<br />
<br />
Let's now switch users and try to login as one of our newly created users, Anthony Bastone (abastone), not the administrator Anthony Bastone (a-abastone)
<br />
<br />
<img src="https://imgur.com/3tAJEr5.png" height="80%" width="80%"/>
<br />
<br />
We've successfully logged in as one of our users. In case you want something more concrete, we can open up the command line and run the following command, whoami, and ping the internet one more time.
<br />
<br />
<img src="https://imgur.com/gaP6eZQ.png" height="80%" width="80%"/>

</p>

<br />
<br />

<h2>Conclusion</h2>

The completion of this Active Directory home lab successfully demonstrated the design, implementation, and configuration of an Active Directory environment using Windows Server 2019 and Oracle VirtualBox. By setting up a Domain Controller with dual NICs for both external and internal network communication, configuring DHCP and RAS/NAT services, and deploying a Windows 10 client machine, I was able to achieve a fully functional network setup.
<br />
<br />
The automation of user account creation via a PowerShell script eliminated the tedious process of manual input and ensured the efficient and accurate setup of over 1,000 user accounts. The integration of the Windows 10 client machine into the domain and the successful login and connectivity tests confirmed the proper configuration of the network services and user accounts.
<br />
<br />
Overall, this project provided practical insights and hands-on experience with Active Directory, networking, and automation using PowerShell. Although the lab was relatively simple, mastering the fundamentals will always be beneficial in the long run. The skills and knowledge gained from this project are incredibly valuable for future work in IT infrastructure and systems administration.

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
