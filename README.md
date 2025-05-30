<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups and Examinations of Azure Virtual Machine Communications</h1>
This lession observes the network traffic and network security group features between Windows and Linux virtual machines in Microsoft Azure. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure Virtual Machine's Platform
- Microsoft Windows App
- Various Command-Line Tools
- Various Network Protocols (SSH, RDP, DNS, ICMP)
- Wireshark (Protocol Analyzer)
- Microsoft PowerShell

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
Since I have already created a Microsoft Azure subscription, I began the first step with the construction of two virtual machines (Windows 10 Pro and Linux [Ubuntu 22.04]). I ensured that both of them resided within one resouce group, one location (East US 2), and one virtual network. The inclusion of the same location and virtual network guaranteed that any pings between the said virtual machines (VMs) would automatically connect to one another. 
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
In preparation of the firewall configuration step, I gave a perpetual ping command between the Windows and Linux virtual machines in Powershell. I did this by entering the command "ping" with the Linux private IP address and a "-t." I then went back to Microsoft Azure and into the Linux VM's network settings to its "Network Security Group." From there, I opened the "Settings" and then "Inbound security rules." I continued forward by creating a new rule that established a deny action to any and all ping activity to the Linux virtual machine.
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
The final high-level step began with the observation of SSH (Secure Shell) in Wireshark and Powershell of the Windows VM. I started the process by opening Wireshark, initiating a packet capture, and then filtering for exclusively SSH traffic. I then opened up Powershell and entered the command "ssh labuser@10.0.0.5," thereby joining the SSH command with the Linux username and private IP address. After issuing this command, I followed it by granting permission via the Linux password to access its VM through the Windows VM. I further observed in Wireshark that with each additional command, more and more encrypted packets came through between the server and the client. Lastly, I issued the command of "exit" in Powershell to close the virtual machine's access to the Linux VM.
</p>
<br />

<p>
<img width="858" alt="Screenshot 2025-04-04 at 5 21 31 PM" src="https://github.com/user-attachments/assets/6239c190-d756-4f9d-b12b-1c08b45de977" />
</p>
<p>
The second stage of the last high-level step started with the observation of DHCP (Dynamic Host Configuartion Protocol) in Wireshark and Powershell of the Windows VM. Initially, I found that when I issued the command of "ipconfig /renew" in Powershell, it did not yield the full packet of data in Wireshark. I therefore created a file in Notepad with the commands "ipconfig /release" and "ipconfig /renew." I then stored the file in "Windows C:/ProgramData" under the file name "dhcp.bat" and saved in an "All Files" type. Following on from there, I went back to Powershell and entered "cd c:\programdata" > "ls" > and then ".\dhcp.bat." These actions then relaunched the Windows VM and renewed the DHCP data traffic in Wireshark. I finally concluded this stage with a complete observation of the assignment steps in DHCP.
</p>
<br />

<p>
<img width="857" alt="Screenshot 2025-04-05 at 3 44 10 PM" src="https://github.com/user-attachments/assets/74b729cc-4fea-40bf-bccb-64daf48c6c98" />
</p>
<p>
The third stage in this high-level step pertained to the observation of DNS (Domain Name System) traffic with the tools of Wireshark and Powershell. I therefore began by restarting the current capture from Wireshark, and then I filtered it down to just "dns." I then entered the command "nslookup" with the hostname of one website (disney.com) into Powershell to obtain its own IP address. I finished by observing the incoming DNS packets captured from Wireshark.
</p>
<br />

<p>
<img width="1193" alt="Screenshot 2025-04-05 at 3 58 41 PM" src="https://github.com/user-attachments/assets/4e3830b4-0df2-4c1d-a101-f05cbe82b956" />
</p>
<p>
The fourth and final observational stage focused on accessing RDP (Remote Desktop Protocol) traffic from Wireshark. I simply cleared the current capture and entered the filter of "tcp.port ==3389" into the top space bar. I then witnessed a long and continuous packet capture from the actual Windows 10 computer to its remote desktop.
</p>
<br />
