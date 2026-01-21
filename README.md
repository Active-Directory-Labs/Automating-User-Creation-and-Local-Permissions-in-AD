# Automating-User-Creation-and-Local-Permissions-in-AD

<h1>Active Directory Management using PowerShell</h1>

<h2>Description</h2>
This lab is a practical guide to managing Windows Active Directory using PowerShell, focusing on automating user creation as well as configuring local permissions to grant system to Domain Users.
<br />


<h2>Utilities Used</h2>

- <b>Azure</b>
- <b>Powershell</b> 
- <b>Active Directory</b>

<h2>Environments Used </h2>

- <b>Windows Server 2022</b>
- <b>Windows 10 Enterprise</b>

<h2>Prerequisites </h2>

- <b>An Azure Account/Subscription (paid or free)</b>
- <b>Pre-created Resource Group in Azure</b> <br/>
    (See Lab: <a href="https://github.com/Active-Directory-Labs/Building-a-Foundational-AD-Environment-in-Microsoft-Azure/blob/main/README.md"> See "Creating the Resource Group" Section</a>)
- <b>2 Pre-created Windows Virtual Machines(VM) on the same subnet in Azure (1 Windows Server 2022 VM + 1 Windows 10 Enterprise VM) </b> <br/>
    (See Lab: <a href="https://github.com/Active-Directory-Labs/Building-a-Foundational-AD-Environment-in-Microsoft-Azure/blob/main/README.md"> How to create two Virtual Machine(s) in the same subnet</a>)
- <b>One Active/Promoted Domain Controller</b> <br/>
    (See Lab: <a href="https://github.com/Active-Directory-Labs/How-to-deploy-AD-and-create-OUs-and-Users/blob/main/README.md#promoting-dcdc-1a-virtual-machine-to-actual-domain-controller"> How to Promote a Virtual Machine to a Domain Controller</a>)

<h2>Keywords </h2> 

- <b>OS = Operating System </b> </br>

- <b>OU(s) = Organizational Unit(s)</b> </br>

- <b>VM = Virtual Machine</b> </br>

- <b>AD = Active Directory</b> </br>

- <b>ADUC = Active Directory Users and Computers</b> </br>

- <b>DNS = Domain Name Server</b> </br>

- <b>DC = Domain Controller</b> </br>

- <b>VNet = Virtual Network</b> </br>

- <b>RG = Resource Group</b> </br>


<h2>Labs walk-through:</h2>

<h3>Initialize the Domain Controller:</h3>

<p align="center">
1. Log in to your Domain Controller VM. You do this because Azure-created Domain Controllers have NLS and require authentication from the Domain Controller on login, so if the DC is off, the user cannot/will not be authenticated in the Domain Controller and therefore will not be provided access: <br/>
<img src="" width="80%" alt=""/>
<br />
<br />
</p>

<h4>Provisioning Global Access to the Client VM:</h4>

<p align="center">
2. In the Client VM, log in as an Admin Account, or an account under Domain Admins Security Group, and go to settings and then "About". In the About settings, click on Remote Desktop:
    <br/>
<br/>
<img src="" height="80%" width="80%" alt=""/>
<br />
<br />
</p>

<p align="center">
3. In the Remote Desktop Settings, click on "Select users that can remotely access this PC":  <br/>
<img src="" height="80%" width="80%" alt=""/>
<br />
<br />
</p>

<p align="center">
4. In the Remote Desktop window, click on "add" to add a new user or OU/group that will be allowed to access this pc:<br/>
<img src="" height="80%" width="80% alt=""/>
<br />
<br />
</p>

<p align="center">
5. In the pop-up window, add Domain Users and click on Find Names. Once the names are found, click on OK to set the new users. The reason we add Domain Users to the list of allowed users for Remote Desktop on the Client/Computer is so that we are not always forced to log in using only accounts that have access to the Computer. Adding Domain Users will allow us to log in as any user as long as that user is a part of the domain, meaning any employee of the company can log in, even newly created employees/users, thus not forcing us to individually give access to this client/computer to each user. This would regularly be done on Group Policy.
:  <br/>
<img src="" height="80%" width="80%" alt=""/>
<br />
<br />
</p>
<p align="center">
6. Once everything is done, click on OK to apply the new settings:  <br/>
<img src="" height="80%" width="80%"/>
<br />
<br />
</p>

<p align="center">
7. Once done, log out of the Admin Account on the Client VM: <br />
  <br/>
<img src="" width="80%"/>
<br />
<br />
</p>

<h3>New User Creation using Powershell:</h3>

<p align="center">
8. Now we have to check if any user can access the Client VM. To do so, we first need to create new users. To create users in bulk, go to the DC VM Open ADUC and Powershell ISE, run Powershell as Admin.: <br />
  <br/>
<img src="" height="80%" width="80%"/>
<br />
<br />
</p>

<p align="center">
9. Copy this code<a href=""> Link to code</a> into the PowerShell file console. If you can't see the console, click on the icon represented by a document with a star logo in the top-left corner. <br />
  <br/>
<img src="" height="80%" width="80%"/>
<br />
<br />
</p>

<p align="center">
10. After pasting the code, save it as a file on the desktop: <br />
  <br/>
<img src="" height="80%" width="80%"/>
<br />
<br />
</p>


<p align="center">
11. Before running the code, make sure that you have a pre-created OU named _EMPLOYEES in ADUC. This will allow the code to have a place to save the new users beside the Domain Users OU: <br />
  <br/>
<img src="" height="80%" width="80%"/>
<br />
<br />
</p>

<p align="center">
12. Press enter to run the code, and if everything worked correctly, you should see new users being populated on the console: <br />
  <br/>
<img src="" height="80%" width="80%"/>
<br />
<br />
</p>

<p align="center">
13. Under the created _EMPLOYEES OU, you should now also see the new users populated in the OU: <br />
  <br/>
<img src="" height="80%" width="80%"/>
<br />
<br />
</p>

<p align="center">
14. If you feel that enough accounts have been populated in the _EMPLOYEES OU, you can stop the code: <br />
  <br/>
<img src="" height="80%" width="80%"/>
<br />
<br />
</p>

<p align="center">
15. Take one of the new user names and try to log in to Client1 using Password1: <br />
  <br/>
<img src="" height="80%" width="80%"/>
<br />
<img src="" height="80%" width="80%"alt="15.0"/>
<br />
</p>

<p align="center">
<b> And you're done, you have now successfully allowed Global Domain Log in to a client VM/Computer and created new users using PowerShell. Don't forget to disable/stop your virtual machine on Azure once done(remember you pay as you use): </b>  <br/>
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


