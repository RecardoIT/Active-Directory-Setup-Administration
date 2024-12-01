## Windows Server 2022: VM & AD Setup⚙️

## Objective
This GitHub project provides a homelab environment within a virtual machine, enabling users to set up an Active Directory domain and explore various IT-related tasks. It's designed to offer a safe testing space without risking damage to internal systems, making it perfect for learning and experimentation.

### Skills Learned
- Active Directory Installation: Skilled in installing and configuring AD DS on Windows Server.
- User & Group Management: Expertise in managing users, OUs, and groups in AD.
- DNS/DHCP Configuration: Knowledge of setting up DNS and DHCP for AD services.
- Troubleshooting & Diagnostics: Skilled in resolving AD issues, including login and replication problems.
- Backup & Recovery: Knowledgeable in creating backups and restoring AD configurations.

### Tools Used

- Oracle VirtualBox: Virtualization platform for creating test environments.
- Active Directory Domain Services (AD DS): Tool for setting up and managing the domain.
- PowerShell: Command-line tool for managing and automating AD tasks.
- Windows Server 2022: Enterprise-level server platform for building and managing Active Directory domains.

## Installing Virtual Machine

First, create a Windows Server 2022 VM. Choose the "ISO image" option, select your Windows Server 2022 ISO, and ensure "Desktop Experience" is checked under the "Type" section in Oracle VirtualBox.

<img src="https://imgur.com/R6Hd4qY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Next, set up an admin username and password for Windows login.
<br>
<img src="https://imgur.com/4KN0ihY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Allocating the right amount of system memory and CPU threads is crucial. My system has 16 GB of RAM and 16 CPU threads. Since the VM won’t run resource-intensive applications, I’ll allocate a quarter of the RAM and CPU threads to ensure smooth performance.
<img src="https://imgur.com/3avB9Lc.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

In Oracle VirtualBox, navigate to the advanced network settings and add a second network adapter, selecting the "Internal Network" option.
<img src="https://imgur.com/Hpzae80.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Proceed with the installation of Windows Server 2022 on the VM.
<img src="https://imgur.com/v8uWdDq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

## Configuring Network Adapters

Once Windows boots, open Settings, navigate to Network & Internet, and select Adapter Settings.
<img src="https://imgur.com/sJxxgsI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Click on an Ethernet adapter, then select Properties. IPv4 address—addresses starting with "10.0.x.x" (e.g., 10.0.8.12) indicate the NAT adapter.
<img src="https://imgur.com/8isXdtW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>


Rename the second network adapter to "Internal" to clearly differentiate between internal network traffic and traffic through the NAT adapter.
<img src="https://imgur.com/T3uXGU4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

## Installing Active Directory

Now, we're ready to install Active Directory. Search for "Server Manager" in the Windows search bar and open it.
<img src="https://imgur.com/4BQZC7i.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Click on the "Manage" tab, then select "Add Roles & Features". Make sure to check the "Active Directory Domain Services" checkbox to ensure proper installation of the directory.
<img src="https://imgur.com/iuwVoXs.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Click Next through any further prompts, and then click the "Install" button when you reach the results page.
<img src="https://imgur.com/dAFzyPp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

A new page will open. Check "Add a new forest" and enter the name for your new local domain. Be sure to add .local at the end of your chosen name to create an internal domain.
<img src="https://imgur.com/nGw4CzN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Continue clicking Next on the following prompts, then click the "Install" button on the "Prerequisites Check" page.
<img src="https://imgur.com/nGw4CzN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

You will be prompted to restart your machine. If not, manually press the Windows logo, select the power button, and restart your machine. After restarting, the system will apply the necessary settings.
<img src="https://imgur.com/UzIzOVm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Open Server Manager again, you'll see that Active Directory Domain Services (AD DS) is marked green.
<img src="https://imgur.com/gxBpXHt.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

## Organising Active Directory

Click on the Windows search icon, type "user", and select "Active Directory Users and Computers".
<img src="https://imgur.com/FPkDpOE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

This will open a window where you can see the local domain you created earlier (e.g., testdirectory.local). Left-click on the domain, and you'll see an array of Organizational Units (OUs).
<img src="https://i.imgur.com/U7ytgp0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Think of Organizational Units (OUs) as folders in Windows. They help keep Active Directory organized and allow separation of different entities within a domain. Right-click on testdirectory.local, hover over New, and select Organizational Unit to create your own.
<img src="https://i.imgur.com/MBR6mcC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Name the first Organizational Unit "UK", then create two more OUs: "USA" and "ASIA".
<img src="https://i.imgur.com/gIqbRPY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Right-click the "UK" OU and create three OUs: "Computer", "Users", and "Server". Repeat for the "USA" and "ASIA" OUs. Your domain structure will now resemble a real business environment!
<img src="https://i.imgur.com/K0Swxs3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Now, let's create a group. Right-click on any of the "Users" Organizational Units you created, select "New", then choose "Group". Groups are used to organize and manage large numbers of users efficiently!
<img src="https://i.imgur.com/TEhGdX2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

When creating a user, provide their first name and last name. For example, if your group is called "Admins" and you want to add multiple admin users, you might set the user's login name to something like a-sstone. If you're adding a new user named "Adam Smith", their login name could be a-asmith to maintain consistency and keep the names neat.
<img src="https://i.imgur.com/tlc22xi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Next, set a password for the new user. I recommend checking "Password never expires", as frequent password changes can lead to users writing down their passwords, which could pose a security risk to the business.
<img src="https://i.imgur.com/v6oRHxr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

To add a user to a group, right-click on the chosen group and select "Properties".
<img src="https://imgur.com/HXipZk1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

In Properties, go to "Members," click "Add," and enter the user's name.
<img src="https://imgur.com/68MtEi9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Finally, press "OK", then click "Apply", and the user will now be added to the selected group!
<img src="https://imgur.com/0MMromZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

## Configuring User & Group Permissions

Next, you'll learn how to secure folders and files to protect them from specific users or groups!
<img src="https://imgur.com/7zgeEya.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

To begin, select the file or folder you want to grant or deny permissions for, right-click it, and choose "Properties". For example, I'll choose my folder called "secret" on the desktop.
<img src="https://i.imgur.com/AVq8vxr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Go to the Security tab. This is where you can manage which specific users or groups have access to the file or folder and set their permissions. Click the Edit button next to "To change permissions".
<img src="https://i.imgur.com/X7AwTAi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

This will open the Advanced Security Settings for the file or folder. Click the Add button, and a text box titled "Enter the object names to select" will appear at the bottom. Type the name of the user or group you want to set permissions for. For example, I'll type in a group I created called "Level 3". Click OK when you're done.
<img src="https://i.imgur.com/11k1ra2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Set permissions below: Full Control grants admin access, and Deny blocks access.
<img src="https://i.imgur.com/8Pl8ozR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>





