<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create a Resource Group
- Create a Virtual Machine
- Observe ICMP Traffic
- Observe SSH Traffic
- Observe DHCP Traffic
- Observe DNS Traffic
- Observe RDP Traffic

<h2>Set up your Virtual Environment</h2>

<p>The first step is to create a resource group for our virtual machines.</p>

![image](https://github.com/user-attachments/assets/52386d4d-d431-4f11-903a-e1772d0d77ee)

<p>Now create your Windows virtual machine. I'd create it in the closest server location nearest you for the best connection and experience.

While creating the VM, select the previously created Resource Group and allow it to create a new Virtual Network (Vnet) and Subnet. Make sure to use the password option under the Administrator Account section:

I'll be using labuser as the username and Cyberlab123! as the password. </p>

![image](https://github.com/user-attachments/assets/fa5ee3e3-7d6e-412a-8296-fe4b4f97573d)

<p>Create an Ubuntu virtual machine.

While creating the VM, select the previously created Resource Group and allow it to create a new Virtual Network (Vnet) and Subnet. Make sure to use the password option under the Administrator Account section.</p>

![image](https://github.com/user-attachments/assets/77d674b4-8a5c-41ea-9489-ddfd989a081a)

<hr>
<h2>Observing ICMP Traffic</h2>

<p>Log in your Windows 10 Virtual Machine, install Wireshark [https://www.wireshark.org/], open it and filter for ICMP traffic only.</p>

![image](https://github.com/user-attachments/assets/72200b07-9d41-4ad9-b835-bf4979e6937a)

<p>Retrieve the private IP address of the Ubuntu VM and attempt to ping it from within the Windows 10 VM. Observe ping requests and replies within WireShark</p>

![image](https://github.com/user-attachments/assets/da94a42a-f1b3-445e-ad87-f594e3bcec37)

![image](https://github.com/user-attachments/assets/52001cbc-8744-4b6b-8977-92300d7aa28d)

<p>Attempt to ping a public website (such as www.google.com) and observe the traffic in WireShark:</p>

![image](https://github.com/user-attachments/assets/8c2a4bf8-8a6a-4412-8313-5ca5f17d117d)

<p>Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM</p>

![image](https://github.com/user-attachments/assets/f5ed556b-90e3-4d44-bc38-3b7063998324)

<p>Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic, while back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity</p>

![image](https://github.com/user-attachments/assets/c40bd9c9-3524-46cd-b038-be1988c188b2)

![image](https://github.com/user-attachments/assets/937da335-45b3-4f7e-9674-1ea4032e8b88)

<p>Re-enable ICMP traffic for the Network Security Group in your Ubuntu VM and back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line ping activity. Finally, stop the ping activity.</p>

![image](https://github.com/user-attachments/assets/557050ef-676c-4c36-a9a8-c0b50743eccf)

<hr>
<h2>Observing SSH traffic</h2>

<p>Back in Wireshark, filter for SSH traffic only and from your Windows 10 VM, “SSH into” your Ubuntu virtual machine (via its private IP address). Type commands (ls, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark.

Exit the SSH connection by typing ‘exit’ and pressing [return]</p>

![image](https://github.com/user-attachments/assets/c5fff836-b14f-4976-8779-89392c75286a)

<hr>
<h2>Observing DHCP Traffic</h2>

<p>Back in Wireshark, filter for DHCP traffic only. From your Windows 10 VM, attempt to issue your VM a new IP address from the command line (ipconfig /renew)

Observe the DHCP traffic appearing in WireShark</p>

![image](https://github.com/user-attachments/assets/73d39bdc-685c-4324-ba24-c61e7a7e3021)

<hr>
<h2>Observing DNS Traffic</h2>

<p>Back in Wireshark, filter for DNS traffic only.

From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com’s IP addresses are and observe the DNS traffic being shown in WireShark</p>

![image](https://github.com/user-attachments/assets/503ddc9f-0ba4-4dea-9bdf-8035473264ff)

<hr>
<h2>Observing RDP Traffic</h2>

<p>Back in Wireshark, filter for RDP traffic only using "tcp.port==3389".

The RDP (protocol) is constantly showing you a live stream from one computer to another, therefore traffic is always being transmitted.</p>

![image](https://github.com/user-attachments/assets/138aa40e-b98b-4ec0-83c9-3e7a74491c98)

<hr>

<p>I hope this tutorial helped you gain a better understanding of network security protocols and how to monitor traffic between virtual machines. This can be done easily on both PC and Mac, with the only extra step on Mac being the download of the Remote Desktop App.

Now that we're finished, make sure to CLEAN UP YOUR AZURE ENVIRONMENT to avoid any unnecessary charges.

Remember to close your Remote Desktop connection, delete the Resource Group(s) you created at the start of the tutorial, and verify that the Resource Group has been successfully deleted.</p>

<hr>
