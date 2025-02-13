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

<h2>Preparing Active Directory Infrastructure in Azure</h2>
<p>
We will implement an Active Directory using Azure Virtual Machines in this lab. 

In Azure, we will create two virtual machines (VMs) in the same resource group and virtual network. One virtual machine will be the Domin Controller (dc-1), and the other will be the Client (client-1). First, create the resource group, then create a virtual network, and make sure the virtual network is in the same resource group you created. Also, when creating the virtual machine, ensure they are in the same region, for example, East. Next, we will create the Domain Controller VM and name it DC -1. When creating the dc-1 VM, choose Windows Server 2022 and size at least two VCPUs.  Create a username and password, then check the box in Licensing.  When you get to Networking, choose the virtual network we created earlier in the lab, select Review, and Create.
</p>
<br />

<p>
  
![Screenshot 2025-02-01 070904](https://github.com/user-attachments/assets/cf348244-18f2-4735-8831-9b932a8b6a3a)

![Screenshot 2025-02-01 071019](https://github.com/user-attachments/assets/81392102-5bfd-48ee-b536-ddf6cbd34195)

![Screenshot 2025-02-01 071059](https://github.com/user-attachments/assets/d82443e2-cbcc-464c-88f4-b44f65a95be6)

![Screenshot 2025-02-01 071140](https://github.com/user-attachments/assets/21e4da7e-9f93-4faa-8c10-eec04cbb3a65)

![Screenshot 2025-02-01 071317](https://github.com/user-attachments/assets/e92f5cb4-faf0-4fd8-94c5-3ed33de202e7)

![Screenshot 2025-02-01 071803](https://github.com/user-attachments/assets/7aa4bf39-3246-4c4c-a109-dabba5f9a6a3)

![Screenshot 2025-02-01 072301](https://github.com/user-attachments/assets/7ef026e8-5628-4a27-b365-2cd4a90ffd1f)
![Screenshot 2025-02-01 072349](https://github.com/user-attachments/assets/63b67991-1e8f-46fd-8f96-37baf8736ff9)
![Screenshot 2025-02-01 072415](https://github.com/user-attachments/assets/da461938-2476-4780-8161-de16e511ca01)
![Screenshot 2025-02-01 072517](https://github.com/user-attachments/assets/263987ad-e751-404e-a411-e58d06a073f5)

</p>
<p>
 Next, we will create the client's virtual machine. For the client’s VM named client -1, select the same region as the dc-1 VM; for Image, use Windows 10 Pro, version 22H2; for size, use two VCPUs. Create a username and password, then choose the same virtual network as dc-1 for networking. Select review and create.
</p>
<br />

<p>
  
![Screenshot 2025-02-01 073311](https://github.com/user-attachments/assets/5a47c251-7282-4dbe-862e-3e43c4e14c28)

![Screenshot 2025-02-01 073337](https://github.com/user-attachments/assets/ea639417-8b22-40a7-8966-b6eb9660f243)

![Screenshot 2025-02-01 073401](https://github.com/user-attachments/assets/ef8c80f2-7626-4bf6-9914-241b150b03b8)

![Screenshot 2025-02-01 073428](https://github.com/user-attachments/assets/ee3aadc2-9033-4e17-9137-bdcd19f2f39b)

</p>

<p>
In the dc-1 VM, we will set the private IP address to static. We have set the IP address to static because client-1 uses the dc-1 server. If that changes, the DNS settings for client -1 will no longer be valid. Go to the dc -1 virtual machine, networking, networking settings, and select Network interface/IP configuration. Click ipconfig1, choose static in Private IP address settings Allocation, and save.
</p>
<br />

<p>
  
![Screenshot 2025-02-01 074346](https://github.com/user-attachments/assets/07b4408f-58c8-4206-8823-53d8c8ad2bf4)

![Screenshot 2025-02-01 074434](https://github.com/user-attachments/assets/3eb21136-374a-4f9f-a3eb-8f66944ed1f5)

![Screenshot 2025-02-01 074524](https://github.com/user-attachments/assets/12b960fd-3283-468e-86b6-33f71dcaaef7)

![Screenshot 2025-02-01 074558](https://github.com/user-attachments/assets/c09deeed-c77b-45e6-8b69-a28ef5d6e858)

![Screenshot 2025-02-01 074621](https://github.com/user-attachments/assets/8611ea75-a466-471a-9530-6d887bc05c3f)

</p>
<p>
Log into dc-1 and disable the Windows Firewall for connectivity testing. Right-click the start menu, run, and type wf.msc. Click on Properties, turn off, apply, and okay.
</p>
<br />

<p>
  
![Screenshot 2025-02-01 075327](https://github.com/user-attachments/assets/eb80c8b1-cca5-42be-9006-f66cb4488576)

![Screenshot 2025-02-01 075438](https://github.com/user-attachments/assets/c11097af-41d0-4fe2-a93a-b3f28782025d)

</p>
<p>
The Client VM DNS needs to be pointed to the Domain Controller. In Azure, go to the  dc-1 VM and copy its private IP address. Next, go to client -1 VM Network settings and select the Network interface/IP configuration. On the left side, click on DNS Servers, choose Custom, paste the DNS Server IP address from dc- 1, and Save. Restart client - 1 VM.
</p>
<br />

<p>
  
![Screenshot 2025-02-01 075729](https://github.com/user-attachments/assets/9507ba3f-9ec3-4b4b-8ddf-5914839f34a7)

![Screenshot 2025-02-01 075812](https://github.com/user-attachments/assets/1b92c34c-4b2b-44f5-af58-3ea53bb4de80)

![Screenshot 2025-02-01 075855](https://github.com/user-attachments/assets/d2a3ca86-8906-4914-b574-91df375b6854)

![Screenshot 2025-02-01 080012](https://github.com/user-attachments/assets/433603e1-837f-4e82-bbf7-0e86f0917d5b)

</p>
<p>
Log in to client -1 and ping dc-1 to ensure a successful connection. Make sure to get dc-1's private IP address. Open Powershell, type in ping, then private IP address, and hit Enter. It should start to ping.
</p>
<br />

<p>

![Screenshot 2025-02-01 081657](https://github.com/user-attachments/assets/d762d69d-40ab-40b4-ae15-c4e60d0fe5af)

</p>
<p>
Run in the PowerShell ipconfig/all; dc-1 private IP address should be seen in the DNS settings in the client-1 VM.
</p>
<br />

<p>
  
![Screenshot 2025-02-01 082006](https://github.com/user-attachments/assets/3d9f8e43-fbe7-4d9e-af88-4e8bdbb25268)

</p>




<h2>Deployment and Configuration Steps</h2>

<p>
In this portion of the lab, we will install Active Directory on the Domain Controller (dc-1). Open dc-1. Go to Windows Start and select Server Manager. In the Dashboard, click on Add Roles and Features. When you get to Server Roles, select Active Directory Domain Services and click on Add Features. Continue to hit Next until you see Install. Click on Install to start the installation. Once installed, we will configure dc-1 to become a domain controller. 
</p>
<br />

<p>
  
![Screenshot 2025-02-03 132724](https://github.com/user-attachments/assets/77091f5f-5f2e-4415-bc13-10bcbd43e8c9)

![Screenshot 2025-02-03 132902](https://github.com/user-attachments/assets/c7cb65f3-50db-463b-b4d1-587eb790f2c5)

![Screenshot 2025-02-03 133015](https://github.com/user-attachments/assets/8985029b-2844-44b8-b063-010a4618f5f1)

![Screenshot 2025-02-03 133300](https://github.com/user-attachments/assets/f26cada7-1620-48bf-a9bd-cdfd815fa293)

![Screenshot 2025-02-03 133331](https://github.com/user-attachments/assets/258e3571-0cce-45b7-8c94-181e18199b1d)

</p>
<p>
In the Server Manager, a yellow flag at the top right corner promotes this server to a domain controller. Click on it. Select Add a new forest. Write mydomain.com. Click Next. Create a Directory Services Restores Mode(DSRM) password and continue to install it. It will restart the dc-1 VM and wait until the restart is complete before logging back into dc-1.  When logging back into dc- 1, you must use mydomain.com\labuser, and the password is still the same.
</p>
<br />

<p>
  
![Screenshot 2025-02-03 133446](https://github.com/user-attachments/assets/8c12b5a5-cefb-411f-b174-64cadbf5134e)

![Screenshot 2025-02-03 133535](https://github.com/user-attachments/assets/c70c64a5-1718-4ed3-b03f-f8ce1fa536ea)

![Screenshot 2025-02-03 133610](https://github.com/user-attachments/assets/5332e371-574e-422f-968c-8087908ece8a)

![Screenshot 2025-02-03 133736](https://github.com/user-attachments/assets/6065dfba-a25d-4f62-b891-b4aa4b5d9b50)

![Screenshot 2025-02-03 133827](https://github.com/user-attachments/assets/913fbffb-f06c-40d5-a337-2a358a3d52b1)

![Screenshot 2025-02-03 134015](https://github.com/user-attachments/assets/ce9c4406-8845-4556-a2c5-e8a7a778de8f)

</p>
<p>
Create a domain admin user within the domain in Active Directory. In the Windows start menu, select the folder Windows Administrative Tools, then select Active Directory Users and Computer. On the left side, right-click on mydomain.com, choose new, click on Organizational Unit (OU), and type in _EMPLOYEES. Then, create a second OU called _ADMINS.
</p>
<br />

<p>
  
![Screenshot 2025-02-03 135921](https://github.com/user-attachments/assets/35fbb0df-6165-49ca-be5d-6827be1bc72e)

![Screenshot 2025-02-03 135952](https://github.com/user-attachments/assets/e9a231ed-6152-4b86-8f6c-c60d65cc51fb)

![Screenshot 2025-02-03 140050](https://github.com/user-attachments/assets/fe8b8172-1080-478b-ab0a-364e34f61760)

![Screenshot 2025-02-03 140131](https://github.com/user-attachments/assets/188359e8-869e-469e-b15d-1c34b9a11d3d)

![Screenshot 2025-02-03 140205](https://github.com/user-attachments/assets/90adbc1e-581a-495d-8588-45e35d8c8548)

![Screenshot 2025-02-03 140255](https://github.com/user-attachments/assets/977d8ca7-583c-4a8d-92a1-659da191ec7e)

![Screenshot 2025-02-03 140400](https://github.com/user-attachments/assets/a2a125d9-2ba0-43b9-ae82-f4227b020e3f)

</p>
<p>
Let’s add a new employee, Jane Doe, to the _ADMINS folder, right-click New, and select User. The username will be jane_admin(mydomain\jane_admin), and create a password.
</p>
<br />

<p>
  
![Screenshot 2025-02-03 140441](https://github.com/user-attachments/assets/9fddf63d-7f29-4531-a288-ebfabd77db2e)

![Screenshot 2025-02-03 140650](https://github.com/user-attachments/assets/8b7f982a-abfb-4a82-b292-0666c68fe8bf)

![Screenshot 2025-02-03 140721](https://github.com/user-attachments/assets/14a27dcc-896e-4dcf-a0e1-4424fa017617)

![Screenshot 2025-02-03 140813](https://github.com/user-attachments/assets/2fc067a3-45e6-4a72-9ebd-1c3e33ad2448)

![Screenshot 2025-02-03 140921](https://github.com/user-attachments/assets/3311caeb-c8ef-440a-aee2-93f0d5d7991b)

![Screenshot 2025-02-03 141041](https://github.com/user-attachments/assets/099d2503-2b17-4c83-8f5b-691449152069)

</p>
<p>
In the _ADMINS, right-click Jane Doe, go to properties, Member Of, Add, type in Domain Admins, hit Okay,  then apply and OK. Jane Doe is now a domain admin. Log out of dc-1 and log back in as “mydomain.com\jane_admin”. 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<h2>Creating Users with PowerShell</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<h2>Group Policy and Managing Accounts</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
