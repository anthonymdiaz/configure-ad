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

- Create the Domain Controller VM
- Create the Client VM
- Ensure Connectivity between the client and Domain Controller
- Install Active Directory
- Create an Admin and Normal User Account in AD
- Create a new organizational unit (OU)
- Create a new employee
- Join Client-1 to your domain
- Setup Remote Desktop for non-administrative users
- Create a bunch of additional users
- Run the script and observe the accounts being created.

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
1. Create the Domain Controller VM (Windows Server 2022) named “DC-1”:

  
  a. Take note of the Resource Group and Virtual Network (Vnet) that get created at this time
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
2. Set Domain Controller’s NIC Private IP address to be static.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
3. Create a Windows 10 VM named “Client-1” using the same Resource Group and Vnet from step 1.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
4. Ensure Connectivity between the client and Domain Controller by logging in to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping -t <ip address> (perpetual ping).
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
5. Log in to the Domain Controller and enable ICMPv4 on the local Windows Firewall.
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
6. Check back at Client-1 to see the ping succeed.
</p>
<br />


<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
7. Install Active Directory:

  
  Log in to DC-1 and install Active Directory Domain Services.<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
8. Promote DC-1 as a DC, setting up a new forest as mydomain.com.</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
9. Restart and then log back into DC-1 as user: mydomain.com\labuser.
</p>
<br />


<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
10. Create an Admin and Normal User Account in AD:
In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”.<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
11. Create a new OU named “_ADMINS”.</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
12. Create a new employee named “Jane Doe” (same password) with the username of “jane_admin”.
</p>
<br />


<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
13. Add jane_admin to the “Domain Admins” Security Group.
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
14. Log out/close the Remote Desktop connection to DC-1 and log back in as “mydomain.com\jane_admin”.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
15. Use jane_admin as your admin account from now on.
</p>
<br />


<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
16. Join Client-1 to your domain (mydomain.com):
From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address.
From the Azure Portal, restart Client-1 after that.<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
17. Log in to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain (computer will restart).</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
18. Log in to the Domain Controller (Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers (ADUC) inside the “Computers” container on the root of the domain.</p>
<br />


<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
19. Setup Remote Desktop for non-administrative users on Client-1:
Log into Client-1 as mydomain.com\jane_admin and open system properties.<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
20. Click “Remote Desktop” and allow “domain users” access to remote desktop.
  
  
  a. You can now log into Client-1 as a normal, non-administrative user now.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
21. Create a bunch of additional users and attempt to log into client-1 with one of the users:

  
  a. Log in to DC-1 as jane_admin.</p>


  b. Open PowerShell_ise as an administrator
<br />



<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
22. Create a new File and paste the contents of the script into it</p>


[https://github.com/anthonymdiaz/Generate-Names-Create-Users.ps1/blob/main/README.md?plain=1
](https://github.com/anthonymdiaz/Generate-Names-Create-Users.ps1/blob/main/README.md?plain=1)
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
23. Run the script and observe the accounts being created. 


  a. When executing the PowerShell script: Make sure you are doing it on Windows Server VM, not the Client VM.
</p>
<br />


<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
24. When finished, open ADUC and observe the accounts in the appropriate OU.
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
25. Attempt to log into Client-1 with one of the accounts (take note of the password in the script)


  a. Finalize any remaining setup tasks and ensure everything functions as expected.
