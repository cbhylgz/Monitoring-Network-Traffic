.<p align="center">
<img src="https://i.imgur.com/VvEfgCC.jpeg" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />

 <h1>Azure - Virtual Machine Setup and Monitoring Network Traffic</h1>

<h2>Description</h2>
This step-by-step guide demonstrates how to create virtual machines and a network, as well as how to monitor network traffic using a network protocol analyzer known as Wireshark, with the use of Microsoft Azure. 
<br />

<h2>Environments and Utilities Used</h2>

- <b>Microsoft Azure</b>
- <b>Virtual Machines</b>
- <b>Remote Desktop Connection</b> 
- <b>Wireshark</b>
- <b>Various Network Protocols (ICMP, SSH, DHCP, DNS)</b>
- <b>Command-Line Tools</b>

<h2>Operating Systems Used </h2>

- <b>Windows 10</b>
- <b>Ubuntu 24.04</b>

<h2>Steps to Take:</h2>

<p align="center">
First, go to Microsoft Azure, navigate to Resource Groups and create one: <br/>
<img src="https://i.imgur.com/CXb8NhX.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Next, go to Virtual Machines and create one:  <br/>
<img src="https://i.imgur.com/BFVxZjp.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Next, get it set up. For this VM, you'll want it to be a Windows 10 Pro image, with 2-4 CPUs, as seen in the following: <br/>
<img src="https://i.imgur.com/wVOFFAk.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
<img src="https://i.imgur.com/ITidP25.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
After creating it, you should have your Windows 10 VM, with all the resources needed to make it run, including an IP. </br>
Now, create the second one. This time, it should have an Ubuntu image: </br>
<img src="https://i.imgur.com/PguX7Mi.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Instead of creating a brand new virtual network, make sure that this VM is on the same virtual network as the first. <br/>
<img src="https://i.imgur.com/QXLXthz.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Going back to the resource group, you can see now that both VMs exist on the same virtual network: <br/>
<img src="https://i.imgur.com/gIWv0pv.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Open up RDP (Remote Desktop Protocol) and use the first VM's (the one with Windows 10 Pro image) public IP address to connect to it:  <br/>
<img src="https://i.imgur.com/uBvHBXK.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Once connected, open up the browser and navigate to Wireshark's URL to download it:  <br/>
<img src="https://i.imgur.com/lfj12DA.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Once installed, click "Ethernet" to monitor the traffic on the network:  <br/>
<img src="https://i.imgur.com/qCIJYSG.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Type "ICMP" at the top of Wireshark's bar to filter for ICMP (Internet Control Message Protocol). Afterwards, get the second VM's private IP and use PowerShell to ping it:  <br/>
<img src="https://i.imgur.com/b46hmaD.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
<img src="https://i.imgur.com/MG6FzdI.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Configure the firewall to deny ICMP traffic. First, you will need to ping from PowerShell again:  <br/>
<img src="https://i.imgur.com/HGNy9PE.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Next up, enter the second VM's network security group and create a new inbound security rule to deny all ICMP traffic. Make sure to set the rule to the highest priority:  <br/>
<img src="https://i.imgur.com/H2zVFyt.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Check the first VM. Because of the rule, none of the ICMP echo requests are receiving replies:  <br/>
<img src="https://i.imgur.com/MoFJ39C.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Go to the second VM's network security group again, and this time, switch the inbound rule to "Allow" instead of "Deny": <br/>
<img src="https://i.imgur.com/vBW9VP3.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
This change in the rule now allows the ICMP echo requests to receive responses:  <br/>
<img src="https://i.imgur.com/FPXmXdY.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Next, filter to only show SSH (Secure Shell) traffic by typing SSH into the bar in Wireshark, then, once again using PowerShell, SSH into the second VM. Remember to use the private IP:  <br/>
<img src="https://i.imgur.com/blrFX07.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Feel free to experiment by typing commands and observe how the traffic changes:  <br/>
<img src="https://i.imgur.com/Corgjvn.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Filter for DHCP (Dynamic Host Configuration Protocol) traffic using the bar again, and go for a new IP address by using the ipconfig /renew command in PowerShell:  <br/>
<img src="https://i.imgur.com/Zq7X1Zv.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Filter for DNS (Domain Name System) traffic, then use nslookup to search for IPs for domain names such as "www.google.com":  <br/>
<img src="https://i.imgur.com/3cGR7xZ.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
To conclude, observe RDP (Remote Desktop Protocol) traffic by typing in "tcp.port == 3389" in the top bar. The endless line of traffic is occurring because the RDP is showing you a live stream from one PC to another: <br/>
<img src="https://i.imgur.com/0eQAkky.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
