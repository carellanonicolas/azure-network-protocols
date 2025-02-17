<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, I observe various network traffic to and from Azure Virtual Machines using Wireshark as well as experiment with Network Security Groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (ICMP, SSH, DHCP, DNS, RDP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Step 1: Create our Resource Group and 2 Virtual Machines (VM) in Microsoft Azure. One with Windows 10 and the other with Ubuntu.
- Step 2: Use Remote Desktop to connect to our Windows 10 Virtual Machine and Install Wireshark.
- Step 3: Open Wireshark and filter for ICMP traffic only. Retrieve the private IP address of the Ubuntu VM and attempt to ping it from within the Windows 10 VM. Observe ping requests and replies within Wireshark.
- Step 4: Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu/Linux VM. Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic. Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity.
Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is using. Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity, then stop the ping activity.
- Step 5: From your Windows 10 VM, “SSH into” your Ubuntu Virtual Machine (via its private IP address), observe traffic then exit SSH.
- Step 6: From your Windows 10 VM, attempt to issue your VM a new IP address from the command line (ipconfig /renew) and observe DHCP traffic in Wireshark.
- Step 7: From your Windows 10 VM within a command line, use nslookup command to see what nike.com is and observe DNS traffic in Wireshark.
- Step 8: Observe ongoing RDP traffic (tcp.port == 3389) in Wireshark.
- Clean up, and delete Resource Groups in Azure.

<h2>Actions and Observations</h2>
<p>
<p>

<h3>Step 1: Create Resource Groups and Virtual Machines</h3>
One requirement for this lab is to create our Resource Group and two (2) VMs on Azure. One machine will be a Windows 10 (VM1) and the other will be a Linux machine (VM2).<br/>

<p></p>

If you need guidance on how to create VMs in Azure, you can see my tutorial on it [here](https://github.com/Ronaldo-Garcia/Rescource-Groups-and-VMs).

<p></p>

<p></p>


<img src="https://i.imgur.com/jIrniNI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<h3>Step 2: Download Wireshark via RDP on Windows Virtual Machine (VM1) </h3>
<p></p>

Use Remote Desktop to connect to our Windows 10 Virtual Machine (VM1) using the Public IP address and Install [Wireshark](https://www.wireshark.org/download.html) in there.
<p

<p></p>

<img src="https://i.imgur.com/Vq6wpon.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<h3>Step 3: Observe ICMP Traffic</h3>
Once Wireshark was downloaded and Installed in Windows 10 VM (VM1), I opened and filtered for ICMP traffic only. Then using Powershell and the private IP address of the Ubuntu VM (VM2) I attempted to ping it from within the Windows 10 VM and Observed ping requests and replies within Wireshark from both Virtual Machines.

<br />
<p>
<img src="https://i.imgur.com/9qAJ7Q9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<h3>Step 4: </h3>
<p></p>
 
Now, after I Initiated a perpetual/non-stop ping from our Windows 10 VM to our Ubuntu/Linux VM, let's Open the Network Security Group using by the Ubuntu VM, disable incoming (inbound) ICMP traffic and observe the ICMP traffic in WireShark and the command line Ping activity.
<br/>
<img src="https://i.imgur.com/VLuPiCJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
Observe the ping request times out after the firewall rule was implemented (*note - The ping request timed out due to the ICMP traffic being denied as the firewall rule blocked the traffic).
<br />
<img src="https://i.imgur.com/1qmVWEA.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Back to VM2’s Network Security Group to "Allow" the Inbound Security Rule that was set up to deny so the incoming ICMP traffic would be allowed to VM2 again. We can see that Re-enable ICMP traffic for the Network Security Group in Ubuntu VM brings back ping requests and replies within Wireshark. Now we can stop the ping activity by pressing "Control" + "C".
<br />
<img src="https://i.imgur.com/Tcu7L1u.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<h3>Step 5: Observe SSH Traffic </h3>
<p></p>  
  
I then filtered for SSH (Secure Shell) traffic in Wireshark and used the PowerShell terminal to “SSH into” VM2. Connecting to VM2 using SSH, along with typing and executing commands, generated SSH packets that could be observed in Wireshark. Using the “exit” command to end the SSH session.
<br />
<img src="https://i.imgur.com/gD7kvlG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>
<h3>Step 6: Observe DHCP Traffic </h3>
<p></p>
 
To observe DHCP (Dynamic Host Configuration Protocol) traffic which is the network protocol responsible for automatically assigning IP addresses, let's filter for DHCP traffic in Wireshark and used the “ipconfig /renew” command to attempt to issue a new IP address to VM1. Although the private IP address did not change, Wireshark shows that there was a request and acknowledgment, so DHCP traffic was generated.
<br />
<img src="https://i.imgur.com/1COIRiA.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>
<h3>Step 7: Observe DNS Traffic </h3>
<p></p>
I filtered for DNS (Domain Name System) traffic in Wireshark and used the “nslookup” command for www.nike.com. This command basically asks our DNS server what is Nike's IP address. DNS is the network protocol that transforms Fully Qualified Domain Names (FQDNs) into their assigned IP addresses.
<br />
<img src="https://i.imgur.com/3GeBfeC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>
<h3>Step 8: Observe RDP Traffic </h3>
<p></p>
 Finally, I will filter for RDP (Remote Desk Protocol) traffic by using the TCP port number (tcp.port==3389). RDP is the protocol that allows the remote connection to another computer and complete control of the Graphical User Interface (GUI). RDP traffic was continually generated.
<br />
<img src="https://i.imgur.com/bfO6tMe.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
Thank you for checking out this tutorial. It should have helped you gain a better understanding of network protocols and how network traffic works.


**REMEMBER TO DELETE YOUR RESOURCES ONCE YOU ARE DONE WITH THE LAB!**

