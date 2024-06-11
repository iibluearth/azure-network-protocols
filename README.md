# azure-network-protocols
<p align="center">
<img src="https://i.imgur.com/MkZnGcM.png" alt="VM1 Windows and VM2 Linux"/>
</p>

<h1>Network Security Groups (NSG) and Inspecting Traffic Between Azure Virtual Machines</h1>
This tutorial, we will observe various network traffic from Azure Virtual Machines with Wireshark and briefly experiment with Network Security Groups.<br />

<h2>Video Demonstration</h2>

 ### [YouTube: Azure Virtual Machines, Wireshark, Network Security Groups](https://www.youtube.com)

 <h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Command-Line Tool
- Various Network Protocols (SSH, RDH, DNS, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)
- Ubuntu Server 20.04

<h2>List of Prerequisites</h2>

- Install a Windows 10 VM and an Ubuntu VM within the same Resource Group and Virtual Network 
- Install Wireshark
- Experiment with Network Security Groups
- Observe various types of network traffic

 <h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/chyaFyl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
1. Creating Virtual Machines (VMs):

 - Start by creating two virtual machines in the same Resource Group and Virtual Network.

 - The first VM will run Windows 10 Pro, and the second VM will run Ubuntu Server 20.04.

 - Both VMs will have an image size of 2vcpu with 16GiB of memory.

 - Ensure the first VM is deployed before creating the second one.
 
 - Refresh the page before starting the creation of the second VM to ensure the Virtual Network populates correctly.

- Use the credentials: `user:labuser` and `password: Labpassword123`.

</p>
<br />

<p>
<img src="https://i.imgur.com/chyaFyl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 2. Installing Wireshark on VM-1/Windows10:
 
 - Log in to VM-1/Windows10 and download/install Wireshark to monitor network traffic.
 
</p>
<br />

 
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
3. Monitoring Network Traffic with Wireshark:

 - Open Wireshark and click the blue shark icon in the top-left corner to start monitoring network traffic.

- Type "icmp" into the filter box and press enter.

</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
4. Filtering ICMP Traffic:

- As ICMP traffic is being filtered, initially, the results will be empty.

- Ping the private IP of VM-2 from VM-1 to generate ICMP traffic.

- Wireshark should now display this network traffic.

</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
5. Configuring Network Security Groups (NSGs):

- Navigate to the Overview page of VM-2 and go to the Networking tab.

- Add an "Inbound Security Rule" to deny ICMP traffic from any source.

- Specify "ICMP" as the protocol, "Deny" as the action, set the priority to "200", and name the rule "DENY_ICMP_PING_FROM_ANYWHERE".

- After adding the rule, it should appear in the list.

- Optionally, this can also be done from the dedicated "Network Security Groups" page by selecting VM-2 and then "Inbound security rules".

</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
6. Testing the Rule:

- Return to VM-1 and ping VM-2's private IP again.

- This time, the ping request should time out, indicating that the ICMP traffic is blocked.

- In Wireshark, only "requests" will be visible, and no "reply" will be observed.

</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
7. Removing the Rule:

 - Navigate back to VM-2's Network Security Groups and delete the previously added Inbound security rule.

- After a few minutes, pinging VM-2 should work again, and Wireshark will display "reply" traffic.

</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Before concluding this tutorial, let's take a moment to observe the various types of network traffic occurring in the background of our virtual machine (VM).

2. **Filtering Network Traffic**: We can achieve this by filtering through different network protocols.

3. **Examples Demonstrated**: In the images provided above, I've showcased a few examples of filtering through protocols such as "SSH," "DHCP," "DNS," and "RDP" using Wireshark.

4. **Corresponding Traffic Creation**: Additionally, I've utilized the command line to create the corresponding types of traffic for each protocol mentioned.

</p>
<br />