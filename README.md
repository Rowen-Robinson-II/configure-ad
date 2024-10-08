<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of Active Directory within Azure Virtual Machines.<br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 

<h2>Deployment and Configuration Steps</h2>

- Step 1: Create and Connect Virtual Machines: DC-1 and Client-1
- Step 2: Install Active Directory on DC-1
- Step 3: Create a Domain Admin user within the domain
- Step 4: Join Client-1 to domain
- Step 5: Setup Remote Desktop for non-admin users on Client-1
- Step 6: Create users
- Step 7: Configure Group Policy
- Step 8: Enable/Disable accounts

<h2>High-Level Deployment and Configuration Steps</h2>

<h3 align="center">Step 1: Create and Connect Virtual Machines: DC-1 and Client-1</h3>
<p>
<img width="959" alt="image" src="https://github.com/user-attachments/assets/c0bf980b-fde7-4818-9681-cf91097b5101">
</p>
<p>
Two Virtual machines were created one named "DC-1" the other "Client-1" both are on the same virtual network, share the same resource group, and are in the same subnet.DC-1 was deployed with windows server 2022 while Client-1 was deployed with windows 10. Client-1's DNS settings have been configured to DC-1's private IP address.
</p>
<br>
<br>
<br />

<h3 align="center">Step 2: Install Active Directory on DC-1</h3>
<p>
<img width="854" alt="image" src="https://github.com/user-attachments/assets/0af44c0f-1b1a-485a-bb0c-faa0e76ea94a">
</p>
<p>
Login to DC-1 and install Active Directory Domain Services. Promote as a Domain Controller, then setup a new forest as mydomain.com. Restart then log back on using mydomain.com
</p>
<br>
<br>
<br />

<p>
<img width="856" alt="image" src="https://github.com/user-attachments/assets/5bc4fd22-a9de-474a-b665-71ea8aa27292">
</p>
<p>
In Active Directory Users and Computers (ADUC), create Oganizational Units: _ADMINS, _EMPLOYEES, _CLIENTS, _Groups. 
</p>
<br>
<br>
<br />

<h3 align="center">Step 3: Create a Domain Admin user within the domain</h3>
<p>
<img width="853" alt="image" src="https://github.com/user-attachments/assets/f621a3c1-c7fe-48ab-87c5-522b140de59f">
</p>
<p>
Create a new employee named jane doe with the username "jane_admin", then add jane to domain admin security group. 
</p>
<br>
<br>
<br />

<h3 align="center">Step 4: Join Client-1 to Domain</h3>
<p>
<img width="959" alt="image" src="https://github.com/user-attachments/assets/bab40844-d85f-4644-ac06-edbb5fd7c435">
</p>
<p>
login to Client-1 then join mydomain via System Properties then logoff
</p>
<br>
<br>
<br />

<h3 align="center">Step 5: Setup Remote Desktop for non-admin users on Client-1</h3>
<p>
<img width="959" alt="image" src="https://github.com/user-attachments/assets/80a15d51-4bf8-4273-8ddf-9a3cb6762629">
</p>
<p>
login to Client-1 as jane_admin got System Properties -> Remote Desktop. Then add "domain users" access to remote desktop.
</p>
<br>
<br>
<br />

<h3 align="center">Step 6: Create users</h3>
<p>
<img width="959" alt="image" src="https://github.com/user-attachments/assets/637ed5a5-4fba-4fe8-90a3-9f7315d920bd">
</p>
<p>
login to DC-1 as jane_admin, open PowerShell_ise as an admin. Create a new file then paste the contents of the account creator script. once created the accounts can be used to login to mydomain
</p>
<br>
<br>
<br />

<h3 align="center">Step 7: Configure Group Policy to Lockout the account after 5 attempts</h3>
<p>
<img width="959" alt="image" src="https://github.com/user-attachments/assets/51a97893-2f84-4c64-a708-45cb4b9044db">
</p>
<p>
log into DC-1 go to Group Policy Management. Right-Click "Account Lockout Policy". Via Group Policy Management Editor go to Computer configuration -> Policies -> Windows Setting -> Security Settings -> Account Policies -> Account Lockout policy. Configure the lockout settings, then link the policy the the specified domain. Force update the policy using Command Prompt by typing "gpupdate /force"
</p>
<br>
<br>
<br />

<h3 align="center">Step 8: Enabling and Disabling Accounts</h3>
<p>
<img width="958" alt="image" src="https://github.com/user-attachments/assets/84d53f5e-0488-45c0-b001-264dd8a5dee4">
</p>
<p>
To disable/enable an account go to Active Directory Users and Computers find a user in the _EMPLOYEE folder right-click their name then disable/enable as needed
</p>
<br>
<br>
<br />

