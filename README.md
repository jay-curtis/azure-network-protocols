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

- Creation of Windows and Ubuntu (Linux) Virtual Machines
- Installation of Wireshark and Observation of ICMP Traffic
- Configuration of Firewall within Network Security Group
- Observation of Various Kinds of Traffic (SSH, DHCP, DNS, and RDP)

<h2>Actions and Observations</h2>

<p>
<img width="1509" alt="Screenshot 2025-04-03 at 3 17 42 PM" src="https://github.com/user-attachments/assets/b6e5aa02-c14e-4e27-83f0-abbd175c8dd3" />
</p>
<p>
Since I have already created a Microsoft Azure subscription, I began the first step with the construction of two virtual machines (Windows 10 Pro and Linux [Ubuntu 22.04]). I ensured that both of them resided within one resouce group, one location (East US 2), and one virtual network. This inclusion of the same location and virtual network guaranteed that any pings between the said virtual machines (VMs) would automatically connect to one another. 
</p>
<br />

<p>
<img width="746" alt="Screenshot 2025-04-03 at 4 52 18 PM" src="https://github.com/user-attachments/assets/d18db19b-1611-412f-ad5b-f484f3cf7b7e" />
</p>
<p>
I initiated the next step in this process with the download and installation of the Windows App on my MacBook Pro. Once installed, I went to the drop-down menu and selected "Add PC." I then entered the public IP address from the Windows 10 Pro virtual machine. The Windows App further asked me for the administrator credentials that I established when I made the virtual machine. I entered them, and began the next phase of installing Wireshark. I therefore opened the browser, entered Wireshark's website, selected the Windows x64 Installer, and then downloaded the application. I then opened Wireshark and it started capturing packets (as seen above). Lastly, I gave the command of ICMP (Internet Control Message Protocol) in the top search bar, which initially left the window empty.
</p>
<br />

<p>
<img width="902" alt="Screenshot 2025-04-03 at 5 07 07 PM" src="https://github.com/user-attachments/assets/938e5ad7-fd20-4ddd-ab03-4753fd04bc88" />
</p>
<p>
As the image above has indicated, I subsequently opened Powershell in the Windows virtual machine, and then sent the command to ping the private IP address of the Linux (Ubuntu 22.04) virtual machine. Wireshark then automatically started listing the request and reply messages between the Windows and Linux virtual machines, because of my previous command for ICMP data.
</p>
<br />

<p>
<img width="927" alt="Screenshot 2025-04-03 at 6 14 03 PM" src="https://github.com/user-attachments/assets/9eeecb23-50b3-4105-aef8-b67ff1499432" />
</p>
<p>
In preparation of the third step of firewall configuration, I gave a perpetual ping command between the Windows and Linux virtual machines in Powershell. I did this by entering the command "ping" with the Linux private IP address and a "-t." I then went back to Microsoft Azure and into the Linux VM's network settings to its "Network Security Group." From there, I opened the "Settings" and then "Inbound security rules." I continued forward by creating a new rule that established a deny action to any and all ping activity to the Linux virtual machine.
</p>
<br />

<p>
<img width="927" alt="Screenshot 2025-04-03 at 6 14 39 PM" src="https://github.com/user-attachments/assets/8ebf966c-01d6-4bb3-8d56-4b51613b8092" />
</p>
<p>
Having observed through Powershell that the communication between the virtual machines "timed out," I decided to re-enter the Linux settings and delete its new rule. It was then only a few moments later that Wireshark and Powershell began listing the ICMP traffic once again. I ultimately ended the communication session between the virtual machines by entering "Control-C" in Powershell.
</p>
<br />

<p>
<img width="997" alt="Screenshot 2025-04-04 at 3 45 16 PM" src="https://github.com/user-attachments/assets/b2c89363-1b65-41d1-b3c4-8644e23849d8" />
</p>
<p>
The final high-level step began with the observation of SSH (Secure Shell) in Wireshark and Powershell. I started the process by opening Wireshark, initiating a packet capture, and then filtering for exclusively SSH traffic.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
