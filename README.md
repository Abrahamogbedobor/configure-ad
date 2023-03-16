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

STEP2 (Ensuring Connectivity between Client and Domain Controlleer):
- Login to Client-1 and ping DC-1 IP address using ping -t
- Login to DC-1 and enable ICMPv4 on local window firewall
- Revisit Client-1 to see successful pinging to DC-1

STEP3 (Installing Active Directory):
- Longin to DC-1 Server Management Dashboard, and install Active Directory Domain Services
- 

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
<img src="https://i.imgur.com/WhZ700X.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
DC-1 NIC private IP has been changed from dynamic to static thus, client-1 was then logged into and an attempt was made to ping DC-1 IP address from Clinet-1. Unfortunately, the pinging was unsuccessful as shown above. The reason was due to DC-1 not allowing icmp ping (NOTE: icmp is the protocol used in pinging) hence, the preceeding figures was used to show the process used in allowing icmp pings on DC-1 firewall with the aim of allowing connectivity between both VMs.
</p>
<br />

<p>
<img src="https://i.imgur.com/EOniZZG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/Yz8k0eo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/cgWVi67.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/QI66Cja.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The second stage of on-premise active directory configuration on azure is ensuring client one computer (window 10) can ping domain controller computer. First, DC-1 was connected to Micrsoft-RDC using its public IP meaning, two remote desktop computers was running. Second, DC-1 LOCAL firewall was open on search tab where several icmp protocols were enabled after clicking 'inbounding rules' as shown on figure2. As soon as icmp protocols was enabled client-1 pinging started coming through as shown above.
</p>
<br />

<p>
<img src="https://i.imgur.com/lbAt99a.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/gMwoHoO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In order to install Active Directory on DC-1 computer. first, the link that says add roles and features on server management dashboard was entered. Second, DC-1 computer was selected before continuing with the installation. Note, after the installation of Active Directory, 
</p>
<br />

<p>
<img src="https://i.imgur.com/RJHw6cK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/61kdAcb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/1bpE5mP.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/Gb1084h.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Note after the installation of Active Directory Domain Services, the server then needed to be promoted into a Domain Controller using the little yellow flag at the far right end of the dashboard as shown above. That is the point where a domain name was then setup such as (bryanogbe.com) with a publishing password (Password1). To complete this installation, 'add forest' was selected then any domain name with password was chosen as shown above. Finally, installation was completed with automatic log off and VM restart.
</p>
<br />

<p>
<img src="https://i.imgur.com/d2TZzN0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Furthermore, users needed to log back to DC-1 using its public IP address and login details. Unfortunately, the login was unsuccessfuly as shown above because DC-1 is now a doman controller thus, using the innitial login crendetial has been modify. Therefoire, the context of the user trying to login must be specify such as 'bryanogbe.com\bryanlab'
</p>
<br />

<p>
<img src="https://i.imgur.com/uiHCM6O.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/SVqP3EL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After successful login, the above figures were used to show how active directory was deployed as well as how organsiational unit users accounts were created as shsown above. Notably, organisatinal unit are like folder used in organisaing things in a company.
</p>
<br />

<p>
<img src="https://i.imgur.com/RjkqWRM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
From the figures above two organisational unit accounts has been created "_EMPLOYEES & _ADMIN". Note, there are couples of generic account that were automatically created when Active Directory was deployed however, it is a bad habit using those generic account for administrative task in a organisation.
</p>
<br />

<p>
<img src="https://i.imgur.com/RjkqWRM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/mF4hrVE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Bryanlab is the name of the administrative account for this active directory services. In a proper organisational setting assuming i am to work with this platform, i am more likely to create my own administrative accoiunt that is not link with bryanlab as shown above.
</p>
<br />
