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

</p>
<p>
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>

</p>
<p>
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>

</p>
<p>
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>

</p>
<p>
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>

</p>
<p>
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>

</p>
<p>
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>

</p>
<p>
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>

</p>
<p>
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>

</p>
<p>
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>

</p>
<p>
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>

</p>
<p>
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>

</p>
<p>
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>

</p>
<p>
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>

</p>
<p>
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>

</p>
<p>
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>

</p>
<p>
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>

</p>
<p>
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>

</p>
<p>
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>

</p>
<p>
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />
