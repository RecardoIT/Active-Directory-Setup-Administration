#Windows Server 2022: VM & AD Setup⚙️

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

## Organising Active Directory

Click on the windows search icon, and search for "user" then click on "Active Directory Users and Computers"
<img src="https://imgur.com/FPkDpOE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

This will open a window, where we can see our local domain that we created earlier, mine for example is "testdirectory.local" Left click on this space, and you will see an array of oragnizational units. 
<img src="https://i.imgur.com/U7ytgp0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Think of Organization Units as folders within windows, they help to keep the active directory tidy, as well as seperate different organisations within a domain. Right click on the "testdirectory.local" hover over new, and click Organizational Unit to create one of our own.
<img src="https://i.imgur.com/MBR6mcC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

To simulate a working enviroment, lets name this organizational unit as "UK" we are then going to follow the same proccess and make two additional organizational units named "USA" & "ASIA"
<img src="https://i.imgur.com/gIqbRPY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

After that, right click on the "UK" organizational unit we just made, and create 3 seperate organizational units inside of it, called "Computer" "Users" "Server" repeat this proccess for the "USA" and "ASIA" organizational units we created earlier. You will now see that our domain begins to grow a structure, just like it would in a real business! 
<img src="https://i.imgur.com/K0Swxs3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Now the complicated part is out of the way, we can move into creating a group. Right click on any of the "users" organizational units we created and select "new" "group" groups are created to hold a vast amount of users neatly, we'll get into adding users to these groups in just a moment!
<img src="https://i.imgur.com/TEhGdX2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

From here, simply give your user a name and surname, here i have used the name "Simon Stone". If your group was called "admins" for example and you wanted to add multiple admin users to the group, then you may want to set the user login name to something like a-sstone. If you added a new user called "Adam Smith" then you could set their login name as "a-asmith" in order to keep the admin names consistent and neat. 
<img src="https://i.imgur.com/tlc22xi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Then, set a password for your new user, i recommend checking "password never expires" as users like to write down their passwords onto paper, and having them write new password every 2 months for example could serve as a security risk to a business!
<img src="https://i.imgur.com/v6oRHxr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Lets make one more user to make sure you have got the hang of it. Right click on one of the "users" organizational units and select "new" "user" lets fill in their information again and set them a password like last time, this time i will create a user in the "USA" organizational unit.
<img src="https://i.imgur.com/v6oRHxr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

This time i will name my user "Max Holloway" and then create another group in our "users" organizational folder called L1 Help Desk like last time. 
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps.png"/>

In order to add a user into a group, right click on a chosen group and click "properties"
<img src="https://imgur.com/HXipZk1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Now, enter the name of the user you wish to join the following group, by typing out their name in the object names section.
<img src="https://imgur.com/68MtEi9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Finally, press "ok" and then the "apply" button, and that users will now be added to your chosen group!
<img src="https://imgur.com/0MMromZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
















































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

## Configuring User & Group Permissions

Lets say you have a folder or specific file that you only want a user, or a group of users to have access to, how do we do this? we'll it is very simple! 
<img src="https://imgur.com/7zgeEya.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

To begin, select the file and folder you want to grant or deny permissions for and right click it, choosing "properties" for example, i am going to choose my folder called "secret" on the desktop. 
<img src="https://i.imgur.com/AVq8vxr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

After that, head to the security tab, this is where you can choose what specific users or groups have access to specific files and their permissions, such as being able to change the name of a file, or modifying its contents completely. Click the edit button next to "to change permissions"
<img src="https://i.imgur.com/X7AwTAi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

This will open the advanced security section of said file or folder. Click on the add button and a text box will show up at the bottom titled "enter the objects names to select" type the name of the user or group you wish to use to set permissions with. I will type in a group i made called "Level 3" click ok when you're done.
<img src="https://i.imgur.com/11k1ra2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

You will then be able to set the permissions of said user or group below. By checking full control, you allow the user or group to have administrator permissions over said file or folder, you can use this to add a specific user or group and click "deny" on the checkbox "full control" for example to deny that user or group from accessing secure files!
<img src="https://i.imgur.com/8Pl8ozR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

In this example, i have given the group "Level 3" full control over the secret folder, and the specific user "Recardo" is denied every permission possible, meaning they will not be able to access this folder anymore.
<img src="https://i.imgur.com/aeq4U3E.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>


