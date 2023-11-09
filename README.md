<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

- Create an Azure Virtual Machine Windows 10

  - Create a Resource Group
  
![AzureStep1](https://github.com/WesGough/osticket-prereqs/assets/150361198/3534546e-bf14-48a1-bb99-a295f82b7621)
  - Create a Windows 10 Virtual Machine (VM) with 2-4 Virtual CPU's
    
![AzureStep2](https://github.com/WesGough/osticket-prereqs/assets/150361198/c1e5eff8-c338-44cc-9831-dd26d223a625)
  - When creating the VM, allow it to create a new Virtual Network (Vnet)
    
![AzureStep3](https://github.com/WesGough/osticket-prereqs/assets/150361198/f69ff5a2-3127-425c-8906-0062a2f164d2)

<h2>Installation Steps</h2>

<p>
<img src="https://github.com/WesGough/osticket-prereqs/assets/150361198/e4eedfd6-2032-4450-8a03-3dea8f495ca0" height="50%" width="50%" alt="Disk Sanitization Steps"/>
</p>
<p>
Open Remote Desktop on your computer and using the virtuals machines ip address, login to the virtual machine using the credentials you made when you created your virutal machine
</p>
<br />


<p>
<img src="https://github.com/WesGough/osticket-prereqs/assets/150361198/7101c58c-3178-41b5-a41f-4513ea062777" height="50%" width="50%" alt="Disk Sanitization Steps"/>
</p>
<p>
We will use these files to install osTicket and some of the dependencies. I’m using this offline version to make sure everyone is using the same version of all the files
https://drive.google.com/drive/u/1/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6
<br />

<p>
<img src="https://github.com/WesGough/osticket-prereqs/assets/150361198/e15c968b-5111-4a5c-9bd1-b41d4f9fab23" height="50%" width="50%" alt="Disk Sanitization Steps"/>
</p>
<p>
Install / Enable IIS in Windows WITH CGI and Common HTTP Features
	
- World Wide Web Services -> Application Development Features -> [X] CGI [X] Common HTTP Features AND IIS Management Console

- Internet Information Services -> Web Management Tools -> IIS Management Console [X] IIS Management Console


From the Installation Files, download and install PHP Manager for IIS (PHPManagerForIIS_V1.5.0.msi)

From the Installation Files, download and install the Rewrite Module (rewrite_amd64_en-US.msi)

Create the directory C:\PHP

From the Installation Files, download PHP 7.3.8 (php-7.3.8-nts-Win32-VC15-x86.zip) and unzip the contents into C:\PHP

If you are still having trouble downloading PHP 7.3.8, please try downloading and installing Google Chrome and doing it from within there. 

From the Installation Files, download and install VC_redist.x86.exe.

From the Installation Files, download and install MySQL 5.5.62 (mysql-5.5.62-win32.msi)
- Typical Setup -> Launch Configuration Wizard (after install) -> Standard Configuration


Open IIS as an Admin

Register PHP from within IIS

Reload IIS (Open IIS, Stop and Start the server)

Install osTicket v1.15.8
Download osTicket from the Installation Files Folder
Extract and copy “upload” folder to c:\inetpub\wwwroot
Within c:\inetpub\wwwroot, Rename “upload” to “osTicket”

Reload IIS (Open IIS, Stop and Start the server)

Go to sites -> Default -> osTicket
On the right, click “Browse *:80”

Note that some extensions are not enabled
Go back to IIS, sites -> Default -> osTicket
Double-click PHP Manager
Click “Enable or disable an extension”
Enable: php_imap.dll
Enable: php_intl.dll
Enable: php_opcache.dll
Refresh the osTicket site in your browse, observe the changes

Rename: ost-config.php
From: C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php
To: C:\inetpub\wwwroot\osTicket\include\ost-config.php

Assign Permissions: ost-config.php
Disable inheritance -> Remove All
New Permissions -> Everyone -> All

Continue Setting up osTicket in the browser (click Continue)
Name Helpdesk
Default email (receives email from customers)

From the Installation Files, download and install HeidiSQL.
Open Heidi SQL
Create a new session, root/Password1
Connect to the session
Create a database called “osTicket”

Continue Setting up osticket in the browser
MySQL Database: osTicket
MySQL Username: root
MySQL Password: Password1
Click “Install Now!”

Congratulations, hopefully it is installed with no errors!
Browse to your help desk login page: http://localhost/osTicket/scp/login.php

End Users osTicket URL:
http://localhost/osTicket/ 

Clean up
Delete: C:\inetpub\wwwroot\osTicket\setup
Set Permissions to “Read” only: C:\inetpub\wwwroot\osTicket\include\ost-config.php

Notes:
Browse to your help desk login page: http://localhost/osTicket/scp/login.php  
End Users osTicket URL: http://localhost/osTicket/ 

Part 3 (Post Installation Setup)
- Configure Roles - Admin Panel -> Agents -> Roles -> Supreme Admin
- Configure Departments - Admin Panel -> Agents -> Departments -> System Administrators
- Configure Teams - Admin Panel -> Agents -> Teams -> Level l Support -> Level 2 Support
- Allow anyone to create tickets - Admin Panel -> Settings -> User Settings (Registration Required: Require registration and login to create tickets)
- Configure Agents (workers) - Agent Panel -> Agents -> Add New -> John or Jane
- Configure Users (customers) - Agent panel -> Users -> Add New -> Karen or Ken
- Configure SLA - Admin Panel -> Manage -> SLA (Sev-A 1 hour, 24/7) (Sev-B 4 hours, 24/7) (Sev-c 9 hours, 24/7)
- Configure Help Topics - Admin Panel -> Manage -> Help Topics (Business Critical Outage) (Personal Computer Issues) (Equipment Request) (Passwork Reset)



Part 4 (Tickets and Ticket Lifecycle)
Just practice creating, triaging, and solving tickets. I recommend watching the video to learn about triaging multiple tickets.
Ticket examples:

- Sev-A (1 hour, 24/7) [entire mobile/online banking system is down] -> SysAdmins
- Sev-B (4 hours, 24/7) [accounting department needs adobe upgrade, broken]
- Sev-B/C (2 hours, business hours) [CFO’s laptop seems a bit slow]

</p>
<br />
