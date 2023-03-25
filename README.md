<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This project outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

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
- Promote Active Directory as a DC (Domain Controller after installation). Then add a new forest such as bryanogbe.com with password
- Automatic restart thereafter, log back to DC-1 using bryanogbe.com\bryanlab with bryanlab original password

STEP4 (Create an Admin and Normal User Account in AD)
- In Active Directory Users and Computers ADUC, create two Organisational Unit (OU) and name it _EMPLOYEES & _ADMINS
- Create a new employee account inside _ADMINS folder with username abraham_admin and password 
- Add abraham_admin to 'Domain Admins' security group
- Logout/Close DC-1 connection (Remember the user of this connection was bryanlab with password as Brianajiri2022)
- Log back to DC-1 connection with bryanogbe.com\abraham_admin with password as password88
- From now on used abraham_admin as the new user admin account

STEP5 (Join Client-1 to the domain created "Bryanogbe.com"):
- From Azure portal set Client-1's DNS setting to DC-1 IP address (First, you could try using Client-1 to join the Domain bryanogbe.com and document the error) The aim is for you to know the reason why you MUST first set Client-1 DNS to DC-1 IP address. 
- Restart Client-1 from Azure portal
- Log back to Client-1 using the original local admin bryanlab and then re-try JOINING Client-1 to DOMAIN (bryanogbe.com)
- Clien_1 has been successfully joined to the domain, there will be system restart

STEP6 (Setup Remote Desktop for non-administrative users on Client_1
- Login to Client_1 as bryanogbe.com\abraham_admin and open 'System Properties'
- Open Remote Desktop
- Allow 'Domain Users' access to remote desktop
- Logout of Client_1 and log back in with the new users
- Now, every non-administrative users in the domain user group can log into Client_1
- NOTE: The remote computer login that added domian users group is normally done in organisation as group policy
- Group policy invilves allowing different users to log into thousands of computers

STEP7 (Create a bunch of additional users and attempt to use them to log into Client_1)
- First, login to DC_1 as abraham_admin
- Open PowerShell_ise as an administrator
- Create a new file on notepad and then copy the content and paste it into PowerShell script
- Run the script and observe users account being created
- When finished, open ADUC and observe the new user acounts in the appropriate OU (Organisational Unit)
- Make an attempt to log into Client_1 with one of the new accounts (Take note of the password)

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
Domain Controller named DC-1 (WINDOW SERVER 2022), has been successfully created after passing its validation test as shown above. Also, several resources such as resource group, virtual network, and subnet were automatically created when creating DC-1 VM. Note, prior to now, Client-1 was using VNET DNS server but that we do not want as we want it to use DC-1 IP address then we can be able to achieve our aim.
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
From the figures above two organisational unit accounts folder "_EMPLOYEES & _ADMIN" has been created on AD. Note, there are couples of generic account that were automatically created when Active Directory was deployed however, it is a bad habit using those generic account for administrative task in a organisation.
</p>
<br />

<p>
<img src="https://i.imgur.com/RjkqWRM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/mF4hrVE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/1h1HBhJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Bryanlab is the name of the administrative account for this active directory domain services. In a proper organisational setting assuming one is to work with this platform, an employee is more likely to create his own administrative account that is not link with bryanlab as shown above. In order to creeate own administrative users account first, the admin folder (organisational units) that was earlier created would be use .
</p>
<br />

<p>
<img src="https://i.imgur.com/teaWkv6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/qvMm2TQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Note: Abraham Ogbe is the new administrative account created inside the _ADMINS folder however, abraham_admin has not gotten any adminstrative function yet although is inside the _ADMIN folder it is ambigous with no meaning yet. The second figure further help to illustrate how an administrative fucntion was added to abraham ogbe after adding it to a domain (bryanogbe.com). Anyone who is a member of the domain admin group can make changes to accounts.
</p>
<br />

<p>
<img src="https://i.imgur.com/wR2eZ1e.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After entering 'DOMAIN' on the box, the following domain accounts group then pop-up as shown above of which 'domain admins' was then selected and applied to finally create a new adminstrative account as abrahaam_admin. Lastly, bryanlab the generic admin was then signed off from DC-1 connection and abraham_admin was later used to sign back making abraham ogbe the new admin user of AD.
</p>
<br />

<p>
<img src="https://i.imgur.com/xybfaUj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The command promt is used to show the new login details and admin user account abraham_admin.
</p>
<br />

<p>
<img src="https://i.imgur.com/CTmwavQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/n6qp1xX.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/IbSFcCE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/GXnZYY6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Client-1 is to be joined to DC-1 Domain (bryanogbe.com) but, before that could be possible, the DNS of Client-1 must be change to the IP address of DC-1. If we failed to change Client-1 DNS setting to DC-1 IP we will have error if we then intend joinng Client-1 to the DOMAIN (bryanogbe.com). The second figure above was used to illustrate why it is important to change client-1 DNS settings. First on Client-1 computer we went through settings and about to rename the PC in advance option. Then, the dialog box in figure two poped-up. After we clicked on change the domain as shown above, we then add Client-1 to a bryanogbe.com DOMAIN. We then recorded the error message we received as shown above. The reason for that error message was because we still using a public DNS on client-1. Therefore, we must first change that to the IP of DC-1.
</p>
<br />

<p>
<img src="https://i.imgur.com/6ioe4Dn.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/qWdfzSl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Changing Client-1 DNS server to DC-1 IP address in order for Client-1 to be able to JOIN AD DOMAIN (bryanogbe.com). First, networking was clicked on Client-1 VM in Aure portal then client-1362 also, DNS servers was selected thereafter, a dialog box appeared that has Client-1 DNS as 'INHERIT' which was finally change to 'CUSTOM' with 10.0.0.4 which was DC-1 IP.
</p>
<br />

<p>
<img src="https://i.imgur.com/NWEzSuZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/xKphXY1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/PHMbWhi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Client-1 DNS has now been change to DC-1 IP address with automatic restart at completion, the above figures was used to test the changes made. Hence, an attemp to JOIN AD DOMAIN (bryanogbe.com) was done the second time which came out successful as shown above. From the figure above, there was no error message this time instead the login details of an administrative account was requested. Meaning, the admin user account that was created previously (abraham_admin) was used to finally complete the JOINING  process. Because, Client-1 has now join the Doman Server hence, abraham_admin will then be able to login to Client-1 computer any time even though he has never use the Client-1 computer before.
</p>
<br />

<p>
<img src="https://i.imgur.com/aZ4W3e8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/7btKksa.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/lGoJH8S.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now, bryanlab has been logged out from Client_1 VM thus, the domain admin user account that was created i.e bryanogbe.com\abraham_admin was then use to login to Clien_1 as shown above. In addition, using system property/About on Client_1 remote computer, some amendment was made to remote desktop whereby users that could remotelty used Client_1 computer was added as shown above.
</p>
<br />

<p>
<img src="https://i.imgur.com/9RPtOqD.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/ugjDYy9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Note: prior to now only domain\admin i.e BRYANOGBE\abraham_ is alowed to login to Client_1 as shown above. Also, the second figure shows how several users are added to a domain user group with the aim of them been able to login to Client_1 computer. By entering the 'Domain Users Group' which is a special security group in Active Directory Domain, this will enable bunch of users to gain access to login to Client_1 insstead of adding users one by one. First a special group called 'Domain Users' was entered then a checked-up was carried out to check the security of the group. This was then populated and underlined, as this then explained who is allowed to login to Client_1 computer BRYANOGBE\Domain Users meaning, all users that will be in that domain. To confirm this user group, the preceeding figure from DC_1 computer shows the domain user group that was added in Client_1 remote desktop.
</p>
<br />

<p>
<img src="https://i.imgur.com/rEazylU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/P2NkGJJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
DC_1 remote computer was connected to using DC_1 public IP in Azure. Then at server management, ADUC (Active Directory Users and Computer) was chosen then users, and domain users group was selected to view all users in the group as shown aove. Furthermore, thousands of users were created on DC_1 using window scripting language (PowerShell ISE), and an attempt was made using them to log into Client_1.
</p>
<br />

<p>
<img src="https://i.imgur.com/JP2ikti.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/9bJ6ETO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The file that was run on PowerShell ise script as shown above contains some code which outline the number of accounts to be created (10000) as well as the password associated with them (Password1). However, users will have the opportunity to change their password when they first log-in but it all depends on the admin running the script. In addition, the script also contain the folder (OU) which the newly created user accounts was stored. Previously, two organisation unit were created _ADMINS and _EMPLOYEES hence, this new users created were all stored inside _EMPLOYEES folder (OU).
</p>
<br />

<p>
<img src="https://i.imgur.com/DcyAkOD.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
As soon as the script is run, bunch of users account were created as shown above and automatically those accounts were dumped inside the _EMPLOYEES folder (OU). Finally, Client_1 was log-out from previous user and one of the newly created users was used to log-back to Client_1. 
</p>
<br />

<p>
<img src="https://i.imgur.com/sY2TSyT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/ID4JDy0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
One of the newly created user account bac.wusi as shown above was used to login to Client_1 computer. Notably, bac.wusi has never logged into Client_1 computer before however, he was able to do that without having any issue. The reason was simply because, Client_1 was joined into Domain Controller also, bac.wusi was also joined into the domain. Therefore, when a request was sent to the domain there was a look-up to check if such user is in the domain.
</p>
<br />

<p>
<img src="https://i.imgur.com/fIIIYa8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/sm1taGI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Finally, users account could be unlocked, rest and diaable form DC_1 meaning, in an instance where a user forget his/her password, domain admin can be able to reset it back with a new password. Also, when users account is locked as a result of wrong input such account canbe unblock. Furthermore, at DC_1 computer user account can be diabled enable back.
</p>
<br />
