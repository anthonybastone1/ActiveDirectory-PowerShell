<h1>Active Directory Home Lab - Adding Users with PowerShell</h1>

<h2>Description</h2>
This Active Directory home lab aims to design, implement, and secure an Active Directory environment using Windows Server 2019 and VirtualBox for virtualization. The project involves setting up a Domain Controller (DC) with dual NICs for outside internet and internal network communication, configuring DHCP and RAS/NAT services, and deploying a Windows 10 client machine for testing. A PowerShell script will automate the management of over 1,000 user accounts, removing the need to input users manually. Lastly, the user accounts are tested to verify successful configuration.

In this project, I created an Active Directory home lab using VirtualBox, Windows Server 2019, and a Windows 10 VM. Configuring and running this lab helped me better understand Windows networking and how Active Directory works. The lab consists of configuring two virtual machines, one acting as the DC that hosts Active Directory with two network adaptors that lead to the outside internet and internal network, and the other being the Client machine where Windows 10 is installed. In the end, over 1,000 users are created with a PowerShell script to streamline the process.

<h2>Key Objectives</h2>

- Design and Implement Active Directory Environment in Server 2019
- Configure Domain Controller and Network Services - DHCP, RAS, NAT
- Automate User Creation with PowerShell
- Deploy Windows 10 Client Machine and Validate

<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b> 

<h2>Environments Used </h2>

- <b>Oracle VirtualBox</b>
- <b>Windows 10 VM (Client Machine)
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
<br /> 
<br />
<br />
Renaming the device to simplify things.
<br/>
<br/>
<img src="https://imgur.com/6uccNNQ.png" height="80%" width="80%"/>
<br />
<br />
<br />
<br />
<br />
Here we see our two network adaptors. Now we need to verify which is for the internet and which is for the internal network, name them appropriately, and configure the proper IP address for the internal network.
<br />
<br />
<img src="https://imgur.com/0Pmiaw3.png"height="80%" width="80%"/>
<br />
<br />
<br /> 
<br />
<br /> 
First, we can check the details of the Ethernet network and look at the IP address. We see it is 10.0.2.15, which would be our home network IP address for NAT. After identifying that, we can go ahead and rename the network to better identify it.
<br/>
<br/>
<img src="https://imgur.com/zyJwDtt.png" height="80%" width="80%"/>
<br />
<br />
<br />
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
<br />
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
<br />
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
<br/>
<br/>
<br/>
After promoting the server to a DC, we are now able to log in to the domain with the built-in admin account.
<br/>
<br/>
<img src="https://imgur.com/M3hEunZ.png" height="80%" width="80%"/>
<br/>
<br/>
<br/>
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
<br/>
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
<br/>
<br/>
<br/> 
Let's verify that we can login to the domain admin account now.
<br/>
<br/> 
<img src="https://imgur.com/r2uxnXn.png" height="80%" width="80%"/> 
<br/>
<br/>
<br/> 
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
<br/>
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
<br/>
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
<br/>  
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
<br/>
<br/>
<br/> 
<br/>
<br/>  
<br/>
<br/>
<br/> 
<br/>
<br/>  
<br/>
<br/>
<br/> 
<br/>
<br/>  
<br/>
<br/>
<br/> 
<br/>
<br/>  
<br/>
<br/>
<br/> 
<br/>
<br/>  
<br/>
<br/>
<br/> 



<h2>Windows 10 (Target Machine):</h2>

<p align="center">
  
<br />
Moving onto the target machine, the first thing I did was change the device name to target-PC.
<br />
<br />
<img src="https://imgur.com/2y2V2Ib.png" height="80%" width="80%"/>
<br />
<br />
<br /> 
<br />
<br />
Next, I used the command ipconfig to take a look at the IP address of the machine. It's set to the address that needs to be used for my Windows Server, so I set a static IP address of 192.168.10.100
<br />
<br />
<img src="https://imgur.com/l9pwBtq.png" height="80%" width="80%"/>
<br />
<br />
<img src="https://imgur.com/dCjwQEj.png" height="80%" width="80%"/>
<br />
<br />
<br /> 
<br />
<br />
After setting the designated IP address, I began installing splunk forwarder. There is no deployment server here, so I only needed to input my splunk server address for the receiving indexer.
<br />
<br />
<img src="https://imgur.com/bYpnVJ9.png" height="80%" width="80%"/>
<br />
<br />
<br />
<br />
<br />
Following the splunk forwarder installation, I downloaded sysmon and used the sysmon configuration by Olaf.
<br />
<br />
<img src="https://imgur.com/XdzyuHw.png" height="80%" width="80%"/>
<br />
<br />
<br />
<br />
<br />
Successfully installed sysmon by running the following command in PowerShell:
<br />
<br />
<img src="https://imgur.com/z5pgWvp.png" height="80%" width="80%"/>
<br />
<br />
<br />
<br />
<br />
Here I created a new inputs.conf file under the local directory and not the default directory. I ran the notepad as an administrator with the following lines of code that instruct the splunk forwarder to push events related to application, security, system, and sysmon over to the splunk server. I have the index pointing to an index named endpoint, so any events that fall under the aforementioned categories will be send to splunk and placed under that specific index.
<br />
<br />
<img src="https://imgur.com/6hgRg2L.png" height="80%" width="80%"/>
<br />
<br />
<img src="https://imgur.com/TPYlOjJ.png" height="80%" width="80%"/>
<br />
<br />
<br />
<br />
<br />
Before restarting splunk forwarder for the changes to take effect, I needed to change the logon setting to logon as a local system account instead of the NT SERVICE account. I did this because the splunk forwarder would not be able to collect logs due to some of the permissions.
<br />
<br />
<img src="https://imgur.com/njRedhb.png" height="80%" width="80%"/>
<br />
<br />
<br />
<br />
<br />
After getting splunk and sysmon successfully installed on the target-PC, I logged onto my splunk enterprise web portal to create my endpoint index.
<br />
<br />
<img src="https://imgur.com/7786WSE.png" height="80%" width="80%"/>
<br />
<br />
<img src="https://imgur.com/kaKeZ2I.png" height="80%" width="80%"/>
<br />
<br />
<br />
<br />
<br />
Once the endpoint index was created, I enabled the splunk server to receive the data.
<br />
<br />
<img src="https://imgur.com/4YjoK2Z.png" height="80%" width="80%"/>
<br />
<br />
<br />
<br />
<br />
Checking to see if the data is being received by the splunk server. Confirming the host machine that's been logged is correct and identifying the categories that I included in the new inputs.conf file in the local directory.
<br />
<br />
<img src="https://imgur.com/uSYZXyg.png" height="80%" width="80%"/>
<br />
<br />
<img src="https://imgur.com/KtaN8ec.png" height="80%" width="80%"/>
<br />
<br />
<img src="https://imgur.com/0PcuSZa.png" height="80%" width="80%"/>
<br />
<br />
<br />
<br />
<br />

<h2>Windows Server (ADDC):</h2>

<p align="center">
  
<br />
To install sysmon and splunk on my Active Directory server, I followed the same steps as the target-PC. The first thing I did was rename the device to ADDC01. In the end, I verified all of my work in the splunk enterprise web portal. Everything was successfully installed and configured, and now two hosts were logged instead of one. The two hosts being the target-PC and ADDC01.
<br />
<br />
<img src="https://imgur.com/8v0eeNs.png" height="80%" width="80%"/>
<br />
<br />
<br />
<br />
<br />
After installing sysmon and splunk, I assigned a static IP address of 192.168.10.7 with the same subnet mask of 255.255.255.0 since it is a /24. Still using Google's DNS of 8.8.8.8.
<br />
<br />
Then I opened the server manager and installed AD DS (Active Directory Domain Services), followed by promoting the server to a domain controller (DC)
<br />
<br />
<img src="https://imgur.com/maOd4eD.png" height="80%" width="80%"/>
<br />
<br />
<img src="https://imgur.com/YMw1hJd.png" height="80%" width="80%"/>
<br />
<br />
<br />
<br />
<br />
Next, I created two organizational units and two users.
<br />
<br />
<img src="https://imgur.com/CfZuJdY.png" height="80%" width="80%"/>
<br />
<br />
<img src="https://imgur.com/k3z188z.png" height="80%" width="80%"/>
<br />
<br />
<br />
<br />
<br />
Joinning the target-PC to the new domain, ab.local, and authenticating using James Brown's account. But first, the target-PC could not resolve ab.local due to the DNS server pointing to Google's DNS. So I changed it to point to the DC at 192.168.10.7 and confirmed with ipconfig /all in the command prompt that the new DNS server is active.
<br />
<br />
<img src="https://imgur.com/CEk89PK.png" height="80%" width="80%"/>
<br />
<br />
<img src="https://imgur.com/wXWtg9E.png" height="80%" width="80%"/>
<br />
<br />
<img src="https://imgur.com/RVnAVty.png" height="80%" width="80%"/>
<br />
<br />
<img src="https://imgur.com/3EBq6D3.png" height="80%" width="80%"/>
<br />
<br />
<br />
<br />
<br />
<h2>Kali Linux VM (Attacker Machine):</h2>

<p align="center">
  
<br />
Assigning a static IP address of 192.168.10.250/24. Verified the change took place by running the command ip a and pinging google.com and the splunk server at 192.168.10.10.
<br />
<br />
<img src="https://imgur.com/Xf6UHpf.png" height="80%" width="80%"/>
<br />
<br />
<img src="https://imgur.com/hKU8CJd.png" height="80%" width="80%"/>
<br />
<br />
<img src="https://imgur.com/ffvCanW.png" height="80%" width="80%"/>
<br />
<br />
<br />
<br />
<br />
Installed updates and upgrades then created a new directory named ad-project. Installed the tool crowbar to use for the brute force attack, and rockyou wordlist to aid in the attack. 
<br />
<br />
<img src="https://imgur.com/GO9FcOj.png" height="80%" width="80%"/>
<br />
<br />
<img src="https://imgur.com/YPqJ5Js.png" height="80%" width="80%"/>
<br />
<br />
<br />
<br />
<br />
Enabled RDP for both users that I created on the Windows machine (target-PC), then conducted the brute force attack in the Kali Linux VM by running the follwoing command:
<br />
<br />
crowbar -b rdp -u jbrown -C passwords.txt -s 192.168.10.100/32
<br />
<br />
Used /32 because I only wanted to target that specific IP address.
<br />
<br />
<img src="https://imgur.com/Sojv0LM.png" height="80%" width="80%"/>
<br />
<br />
<img src="https://imgur.com/tdZrPHg.png" height="80%" width="80%"/>
<br />
<br />
<br />
<br />
<br />
As you can see above, the brute force attack on the user James Brown was successful. So I logged into the splunk web server and queried the database for information related to the attack in the images below. You will notice the event ID 4625 with a count of 20. A quick google search tells us that the event ID 4625 is for failed attempts to log in to a local computer. When I expanded the section, all the attempts occurred at the same time, indicating a brute force attack.
<br />
<br />
There is also an event ID 4624 with a count of 1. This is indicative of a successful attempt to login to a local computer. This also occurred at the same time as the 20 failed attempts, confirming that the successful attempt was part of the brute force attack. So we've seen it from the attacker's side in Kali Linux, and the defender's side in splunk.
<br />
<br />
<img src="https://imgur.com/AUBXxSz.png" height="80%" width="80%"/>
<br />
<br />
<img src="https://imgur.com/McbCFvX.png" height="80%" width="80%"/>
<br />
<br />
<img src="https://imgur.com/ywmI6dT.png" height="80%" width="80%"/>
<br />
<br />
<img src="https://imgur.com/7VmN0Ja.png" height="80%" width="80%"/>
<br />
<br />
<br />
<br />
<br />
Lastly, I set an exclusion for the C drive on the target-PC before installing Atomic Red Team (ART) since Windows Defender can detect and remove some of the files from ART. After doing so, I installed ART.
<br />
<br />
<img src="https://imgur.com/P3CWwJP.png" height="80%" width="80%"/>
<br />
<br />
<img src="https://imgur.com/K6QjNV2.png" height="80%" width="80%"/>
<br />
<br />
<br />
<br />
<br />
Generating telemetry based on creating a local account, NewLocalUser. Searched splunk for NewLocalUser to see if it was detected. Repeated the ART test with another Mitre Att&ck framework technique ID. Both events were detected and they can be used to build alerts based on these activities in the future.
<br />
<br />
<img src="https://imgur.com/iBVk2nw.png" height="80%" width="80%"/>
<br />
<br />
<img src="https://imgur.com/0lQIHCG.png" height="80%" width="80%"/>
<br />
<br />
<img src="https://imgur.com/5JBIbEv.png" height="80%" width="80%"/>
<br />
<br />
<img src="https://imgur.com/TiaJ8p0.png" height="80%" width="80%"/>

</p>

<br />
<br />

<h2>Conclusion</h2>
In this project, I configured four virtual machines. A windows 10 VM, windows server, splunk server, and Kali Linux VM. During the project, I was able to acquire hands-on experience from a multitude of commands, environments, and simulated real-world attacks. I was also able to successfully install sysmon, splunk forwarder, splunk enterprise SIEM, and Atomic Red Team. I've found them to be valuable assets when it comes to cybersecurity as they can help one identity threaths and vulnerabilities within a network. This home lab has equipped me with valuable experience in red teaming and blue teaming. I look forward to continuing to learn and practice the skills necessary for effective security monitoring.

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
