<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

STEP1 (Setting up the Environment):
- Creat Domain Controller VM named 'DC-1' (This is the window server 2022). Notably: Resource Group, Vnet & Subnet will be created along this stage
- Creat Client VM named as Client-1 (Window 10)
- Set Domain Controller's NIC private IP address from dynamic to static
- STEP2 (Ensuring Connectivity between Client-1 and DC-1):
- Login to Client-1 and

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/HYfoaPB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/K19gi11.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Active Directory Domain helps to centrally manage network resources such as user accounts or hardware components such as computers and printers. Notably, the server that powers active directory is called 'DOMAIN CONTROLLER'. The above figures are used to illustrate what would be created in regards to this lab. The first figure shows two virtual machines of which one would be named DC-1 (Domain Controller i.e a server in this lab that will host Active Directory). While the other machine will be named Client-1 preferrably with window 10 that would be use as an organisation computer that any employee could use to login. In figure2, active directory would then be install in DC-1 machine then Client-1 computer will be join to the domain of DC-1 computer as shown above. Finally, bunch of user accounts will be created in DC-1 active directory using 'powershell script'.
</p>
<br />

<p>
<img src="https://i.imgur.com/XRiWAuy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/55hbqEQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Domain Controller named DC-1 (WINDOW SERVER 2022), has been successfully created after passing its validation test as shown above. Also, several resources such as resource group, virtual network, and subnet were automatically created when creating DC-1 VM.
</p>
<br />

<p>
<img src="https://i.imgur.com/0lQMGVK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/GmtD62j.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The figure above shows the steps used in creating the second VM named Client-1 (Window 10). Notable, same resource group used in creating DC-1 was used in creating Client-1 VM. Also, from the second figure both DC-1 and Client-1 were in same Virtual network and subnet as shown above.
</p>
<br />

<p>
<img src="https://i.imgur.com/2jk7TjA.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/GuJf0Qd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/IhVUSbl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The figures above shows the steps used in setting DC-1 NIC private IP address to 'STATIC'. First, from DC-1 VM, networking was selected followed by 'Ip configurations' finally, changes under assignment NIC IP address was then change from dynamic to static as shown above. The effect is that even when the server is switch the IP address will remian the same.
</p>
<br />

<p>
<img src="https://i.imgur.com/S4v7OmW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The NIC priovate IP has been changed from dynamic to static
</p>
<br />
