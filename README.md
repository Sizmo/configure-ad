<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Setup Resources in Azure
- Ensure connectivity between client and Domain Controller
- Install Active Directory
- Create an admin and normal user account in AD
- Join Client-1 to domain
- Setup Remote Desktop for non-admin users on Client-1
- Create additional users and log into Client-1

<h2>Deployment and Configuration Steps</h2>

<h3>Setup Resources in Azure</h3>

<p>
Create Domain Controller VM (Windows Server 2022)
</p>
<ul>
	<li>VM Name: DC-1</li>
	<li>Region: {closest}</li>
	<li>Image: Windows Server</li>
</ul>
<p>
<img src="https://i.imgur.com/nwnKaoR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
Create Client-1 VM
</p>
<ul>
	<li>VM Name: Client-1</li>
	<li>Region: {same as DC-1}</li>
	<li>Image: Windows 10</li>
</ul>
<p>
<img src="https://i.imgur.com/FF47ZeR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
Set DC-1 IP address to static
</p>
<p>
In Azure Portal: Virtual Machine -> DC-1 -> Networking -> Network Interface -> IP configurations -> select ipconfig1
</p>
<p>
<img src="https://i.imgur.com/PmVuIig.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
Ensure both VMs are in the same Vnet
</p>
<p>
<img src="https://i.imgur.com/UK0LV9x.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/QrTwfPu.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<h3>Ensure connectivity between client and Domain Controller</h3>

<p>
Login to Client-1 with Remote Desktop
</p>
<ul><li>Get Client-1's pubilc IP</li><li>Use Remote Desktop Connection with username and password created during setup</li></ul>
<p>
<img src="https://i.imgur.com/wMGMxtL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
Ping DC-1's IP
</p>
<ul></li>Get DC-1's private IP</li><li>Open Command Prompt and ping DC-1</li></ul>
<p>
<img src="https://i.imgur.com/sZ78nNw.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
Login to DC-1 and enable ICMPv4
</p>
<ul><li>Log in to DC-1 using public IP</li><li>Open Windows Firewall</li></ul>
<p>
<img src="https://i.imgur.com/sZp2ppF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Set Inbound Rules
</p>
<p>Inbound Rules -> sort by Protocol -> enable both echo request rules</p>
<p>
<img src="https://i.imgur.com/iDRiQKH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
Check back on Client-1 to see ping succeed
</p>
<p>
<img src="https://i.imgur.com/boOszDv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<h3>Install Active Directory</h3>

<p>
Switch back to DC-1 -> open Server Manager -> Dashboard -> Add roles and features
</p>
<p>
<img src="https://i.imgur.com/C3fMqfw.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
Install Active Directory Domain Services
</p>
<p>
<img src="https://i.imgur.com/0U0dObk.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
Click flag on top right and promote server to domain controller
</p>
<p>
<img src="https://i.imgur.com/5LZNtg3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
Create domain name
</p>
<p>
<img src="https://i.imgur.com/ccBEUYz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
After installing VM will be restarted
</p>
<p>
<img src="https://i.imgur.com/AB4hi7q.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
Re-login to DC-1 using {root-domain-name}/{username}
</p>
<p>
<img src="https://i.imgur.com/pCSKk4y.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<h3>Create an admin and normal user account in AD</h3>

<p>
Open Active Directory Users and Computers
</p>
<p>
<img src="https://i.imgur.com/lpGxlPs.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
Create a new Organizational Unit called "_EMPLOYEES" and one called "_ADMINS"
</p>
<p>
<img src="https://i.imgur.com/NtKXrVb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
In _ADMINS folder, right click and create new user
</p>
<p>
<img src="https://i.imgur.com/9Ri8jkf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
Right click on user and go to properties -> member of -> add -> Domain Admins
</p>
<p>
<img src="https://i.imgur.com/yy0WXvi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
Logout of DC-1
</p>
<p>
<img src="https://i.imgur.com/C9EQFQu.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
Log in with newly created admin user
</p>
<p>
<img src="https://i.imgur.com/ooMJ7ET.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<h3>Join Client-1 to domain</h3>

<p>
Change Client-1's DNS to DC-1's private IP in Azure Portal
</p>
<ul><li>Get DC-1's private IP</li><li>Go to Client-1 -> Networking -> Network Interface -> DNS servers</li><li>Click Custom and paste DC-1's private IP and Save</li></ul>
<p>
<img src="https://i.imgur.com/kSgCgb9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
Restart Client-1
</p>
<p>
<img src="https://i.imgur.com/5sbz2R4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
Join Client-1 to the domain
</p>
<p>Right click start -> System -> Rename this PC -> Change -> Domain -> type {domain name}</p>
<p>
<img src="https://i.imgur.com/u3vwxr2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
Enter admin username and password and restart
</p>
<p>
<img src="https://i.imgur.com/ANFRgRB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<h3>Setup Remote Desktop for non-admin users on Client-1</h3>

<p>
Log in to Client-1 with admin
</p>
<p>Right click start -> System -> Remote desktop -> Select users that can remotely access this PC -> Add -> Domain Users</p>
<p>
<img src="https://i.imgur.com/G8L5EKq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<h3>Create additional users and log into Client-1</h3>

<p>Log in to DC-1 as admin</p>
<br/>

<p>
Open PowerShell ISE as admin
</p>
<p>
<img src="https://i.imgur.com/SymjtLF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
Create new script and paste code from https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1
</p>
<p>
<img src="https://i.imgur.com/TdmUdUn.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>Run the script</p>
<br />

<p>Log in to Client-1 with a random newly created user</p>
<p>
Active Directory Users and Computers -> _EMPLOYEES folder -> right click any user -> Properties -> Account -> copy logon name	
</p>
<p>
<img src="https://i.imgur.com/TL6JzUU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Log out of Client-1 and log in with new username
</p>
