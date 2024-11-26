<h1>VM Home Lab Setup</h1>

 <h2>Description</h2>
A step-by-step guide to setting up a homelab environment in a virtual machine running Windows Server 2022. Learn how to install and configure Windows, create and manage Active Directory, add users, and set up file and folder permissions.

In this section, i will be going over how to set and configure permissions for files, folders and users within windows and active directory.
<br />


<h2>Environments Used </h2>

- <b>Windows Server 2022</b> 

<h2>Program walk-through:</h2>

<p align="center">
Lets say you have a folder or specific file that you only want a user, or a group of users to have access to, how do we do this? we'll it is very simple!  <br/>
<img src="https://imgur.com/7zgeEya.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
To begin, select the file and folder you want to grant or deny permissions for and right click it, choosing "properties" for example, i am going to choose my folder called "secret" on the desktop.    <br/>
<img src="https://i.imgur.com/AVq8vxr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
After that, head to the security tab, this is where you can choose what specific users or groups have access to specific files and their permissions, such as being able to change the name of a file, or modifying its contents completely. Click the edit button next to "to change permissions"  <br/>
<img src="https://i.imgur.com/X7AwTAi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
This will open the advanced security section of said file or folder. Click on the add button and a text box will show up at the bottom titled "enter the objects names to select" type the name of the user or group you wish to use to set permissions with. I will type in a group i made called "Level 3" click ok when you're done. <br/>
<img src="https://i.imgur.com/11k1ra2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
You will then be able to set the permissions of said user or group below. By checking full control, you allow the user or group to have administrator permissions over said file or folder, you can use this to add a specific user or group and click "deny" on the checkbox "full control" for example to deny that user or group from accessing secure files!  <br/>
<img src="https://i.imgur.com/8Pl8ozR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
In this example, i have given the group "Level 3" full control over the secret folder, and the specific user "Recardo" is denied every permission possible, meaning they will not be able to access this folder anymore. <br/>
<img src="https://i.imgur.com/aeq4U3E.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
