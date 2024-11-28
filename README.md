# Active Directory Setup & Administration ⚙️

## Objective
This projects, aims to give a homelab enviroment inside of a virtual machine, allowing the user to create an active directory domain, as well as test various I.T related subjects, without an internal system being potentially harmed in the process. 

### Skills Learned
- Active Directory Installation: Skilled in installing and configuring AD DS on Windows Server.
- User & Group Management: Expertise in managing users, OUs, and groups in AD.
- NS/DHCP Configuration: Knowledge of setting up DNS and DHCP for AD services.
- Troubleshooting & Diagnostics: Skilled in resolving AD issues, including login and replication problems.
- Backup & Recovery: Knowledgeable in creating backups and restoring AD configurations.

### Tools Used

- Oracle VirtualBox: Virtualization platform for creating test environments.
- Active Directory Domain Services (AD DS): Tool for setting up and managing the domain.
- PowerShell: Command-line tool for managing and automating AD tasks.
- Windows Server 2022: Enterprise-level server platform for building and managing Active Directory domains.

## Installing Virtual Machine

First, we will Create the Windows Server 2022 VM. Select the "ISO image" option and select your Windows Server 2022 ISO, make sure to check the desktop expirience under the "Type" section inside of Oracle VirtualBox 

<img src="https://imgur.com/R6Hd4qY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Next, we will setup an admin username and password to boot into Windows with.
<br>
<img src="https://imgur.com/4KN0ihY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

It's important to allocate the right amount of system memory, as well as CPU threads here. My system contains 16GB RAM, as well as a CPU containing 16 threads. Since we are not running any demanding applications on the Virtual Machine, i will allocate a quarter of RAM & CPU threads to be safe.
<img src="https://imgur.com/3avB9Lc.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Within Oracle VirtualBox, i will head to the advanced network tab and create a second network adapter under the option internal network.
<img src="https://imgur.com/Hpzae80.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Installing Windows Server 2022. 
<img src="https://imgur.com/v8uWdDq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

## Configuring Network Adapters

Once Windows boots, go to settings, and then under the "Network & Internet" option, select "Adapter Settings"
<img src="https://imgur.com/sJxxgsI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Now, click on the first ethernet adapter and "Properties" pay attention to the "IpV4 address" an address starting with (example 10.0.8.12) will be the nat adapter 
<img src="https://imgur.com/8isXdtW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Once that's done, rename the second network adapter to "internal" so you can clearly differenciate between the internal network, and traffic going through the nat adapter.
<img src="https://imgur.com/T3uXGU4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

## Installing Active Directory

Now we are ready to install Active Directory, search for "Server Manager" through the Windows search bar and open it.
<img src="https://imgur.com/4BQZC7i.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Click on the "Manage Tab" and then "Add Roles & Features" Make sure to click the "Active Directory Domain Services" checkbox to ensure the directory is installed properly. 
<img src="https://imgur.com/iuwVoXs.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Click next to any further prompts, and click the "Install" button once reaching the results page.
<img src="https://imgur.com/dAFzyPp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

After that, a new page will open, here we are going to check "Add a new forest" and type in the name of our new local domain! Make sure to add .local to the end of your chosen name in order to create an internal domain. 
<img src="https://imgur.com/nGw4CzN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Continue to press next on the following prompts, and then hit the "Install" button on the "prerequisites check" page.
<img src="https://imgur.com/nGw4CzN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

You will then be asked to restart your machine, if not then manually press windows logo, the power button and restart your machine. After doing so, the machine will apply the needed computer settings.
<img src="https://imgur.com/UzIzOVm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Finally, open "Server Manager" again, and if successful your AD DS will be marked green, as well as anything else installed during the creation of your internal domain! 
<img src="https://imgur.com/gxBpXHt.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

