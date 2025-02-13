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

![Screenshot 2025-02-03 141110](https://github.com/user-attachments/assets/8b624772-9e93-401a-8f24-d73712fb9c98)

</p>
<p>
In the _ADMINS, right-click Jane Doe, go to properties, Member Of, Add, type in Domain Admins, hit Okay,  then apply and OK. Jane Doe is now a domain admin. Log out of dc-1 and log back in as “mydomain.com\jane_admin”. 
</p>
<br />

<p>
  
![Screenshot 2025-02-03 141201](https://github.com/user-attachments/assets/edba380f-c0bc-4424-8c29-e0c1bebdc649)

![Screenshot 2025-02-03 141242](https://github.com/user-attachments/assets/971596aa-ccef-47b4-9c9d-165b4c79025c)

![Screenshot 2025-02-03 141317](https://github.com/user-attachments/assets/187ed273-0e55-476c-8c67-acee0735159c)

![Screenshot 2025-02-03 141347](https://github.com/user-attachments/assets/c71b35ba-b4cd-43a2-a1ca-4f1964e1ef51)

![Screenshot 2025-02-03 141424](https://github.com/user-attachments/assets/636dc7b3-a028-40e3-a0f5-b25629722f3a)

![Screenshot 2025-02-03 141450](https://github.com/user-attachments/assets/06bc3e52-2644-4e15-af5c-8e8e3955d96f)

![Screenshot 2025-02-03 141532](https://github.com/user-attachments/assets/68f0b4b7-0ce4-43ee-a7a2-53d5a02dc56c)

</p>
<p>
Log in to Client-1, go to Windows System, Rename this PC(advanced), and click on Change under the computer name tab. Write in Member of Domain: mydomain.com, then OK. Then, write mydomain.com\jane_admin and the password for jane_admin, hit OK, and you should see a pop-up window welcoming you to the mydomain.com domain. The client -1 VM will restart.
</p>
<br />

<p>
  
![Screenshot 2025-02-03 143521](https://github.com/user-attachments/assets/31a63d4a-3195-4c65-8f97-0ee09934d5e5)

![Screenshot 2025-02-03 143622](https://github.com/user-attachments/assets/cd4b571b-9eaa-48bd-bc98-b8e25e55d69c)

![Screenshot 2025-02-03 143706](https://github.com/user-attachments/assets/81e160f3-f2d5-4c20-b1e8-3b40518a2027)

![Screenshot 2025-02-03 143754](https://github.com/user-attachments/assets/2e9c2e10-bc32-43af-ab3d-0b2776c2a2b8)

![Screenshot 2025-02-03 143915](https://github.com/user-attachments/assets/38110b2e-9bba-46b4-9a28-313623220aca)

![Screenshot 2025-02-03 144100](https://github.com/user-attachments/assets/97866cec-ce8e-4d13-96c5-2fa707a3c55f)

![Screenshot 2025-02-03 144147](https://github.com/user-attachments/assets/59d75d4c-0adf-4efd-aaad-a4b1c9cbcda3)

</p>
<p>
Log in to dc-1 and go to Active Directory Users and Computers. Expand mydomain.com, select Computers, and you will see client-1. Create a new OU called _CLIENTS, then drag client -1 into the folder. Refresh mydomain.com; everything created so far should be in its proper folder.
</p>
<br />

<p>
  
![Screenshot 2025-02-03 144414](https://github.com/user-attachments/assets/6728e169-9371-47b6-aca1-40f0e34f1149)

![Screenshot 2025-02-03 144512](https://github.com/user-attachments/assets/a4bd43c3-9d9a-4997-a6ab-088c8456a424)

![Screenshot 2025-02-03 144552](https://github.com/user-attachments/assets/c6b7bb69-acb6-4188-9f0b-f40f5171df25)

![Screenshot 2025-02-03 144626](https://github.com/user-attachments/assets/460630c0-8140-4da1-bc17-5675c0ffc3ce)

![Screenshot 2025-02-03 144738](https://github.com/user-attachments/assets/c31d476c-35bf-45e2-b012-2abe863921d4)

![Screenshot 2025-02-03 144753](https://github.com/user-attachments/assets/2484fbf7-f378-402b-a0fe-771a7014c3c5)

</p>


<h2>Creating Users with PowerShell</h2>

<p>
Log in to client—1 VM as jane_admin. Open system properties and click on remote desktop. Under the user account, select users who can remotely access this PC highlighted. Add Domain Users and hit OK. Now, all users have access to the remote desktop.
</p>
<br />

<p>
  
![Screenshot 2025-02-03 145115](https://github.com/user-attachments/assets/a11907b0-bfb6-45b0-8523-1aa5f4915648)

![Screenshot 2025-02-03 145200](https://github.com/user-attachments/assets/881c7880-a0b6-4b8f-81ca-1f997f3b39d3)

![Screenshot 2025-02-03 145229](https://github.com/user-attachments/assets/1202af1d-c3bd-44de-b6f8-52519710c92d)

![Screenshot 2025-02-03 145414](https://github.com/user-attachments/assets/7757df53-1c88-44e2-9a18-dd876c06db69)

![Screenshot 2025-02-03 145432](https://github.com/user-attachments/assets/91e3d8f1-add1-4a6f-93ac-c6579de27685)

</p>
<p>
Log into dc-1 as jane _admin. Then, open Windows Powershell ISE as an administrator. Create a new file and paste the script provided into it. Save the file as create_users. Click the green arrow to Run the script. The script creates users with different names. 
</p>
<br />

<p>
  
![Screenshot 2025-02-03 145810](https://github.com/user-attachments/assets/c9dba95a-2e89-4723-98ee-a7e41d46c073)

![Screenshot 2025-02-03 150027](https://github.com/user-attachments/assets/48b43988-eaef-4e98-a2c3-a0aab45d0ac4)

![Screenshot 2025-02-03 150041](https://github.com/user-attachments/assets/71035962-5383-4e56-b08c-cfd131a91f24)

![Screenshot 2025-02-03 150104](https://github.com/user-attachments/assets/f4853cc7-1eb2-46b9-817c-df42018d665a)

![Screenshot 2025-02-03 150132](https://github.com/user-attachments/assets/e38b1ac1-26ee-49f4-b471-8c4ec6395430)

![Screenshot 2025-02-03 150310](https://github.com/user-attachments/assets/9cc0eb0d-9a83-40b5-a75e-84881374fa7b)

![Screenshot 2025-02-03 150419](https://github.com/user-attachments/assets/db305c3d-29eb-45ef-9a8a-ef31848ed8ab)

![Screenshot 2025-02-03 155036](https://github.com/user-attachments/assets/6f5d66ac-6c00-49fb-93ab-31dc99fcf933)

</p>
<p>
Once the script is finished, open ADUC and see the _EMPLOYEES folder. Choose one of the users created and login to client-1 VM.
</p>
<br />

<p>
  
![Screenshot 2025-02-03 155403](https://github.com/user-attachments/assets/d46f9dc6-ba0f-4c6b-8b78-708cf82e9c44)

![Screenshot 2025-02-03 160105](https://github.com/user-attachments/assets/6a0e81ea-0e45-4ac1-a528-f76708856f90)

![Screenshot 2025-02-03 160147](https://github.com/user-attachments/assets/74b70052-138a-445b-9001-204b8aee5819)

</p>

<h2>Group Policy and Managing Accounts</h2>

<p>
In this section of the lab, we will learn how to handle account lockouts and password resets. First, we have to set up the account lockout policy in Active Directory. To do this, we will use Group Policy to configure it. 

Login to dc-1. In the start menu, open run and type gpmc.msc, Enter. You are now in the Group Policy Management Console (GPMC). Right-click the Group Policy Objects (GPO) and select New or Edit the Default Domain Policy. 
</p>
<br />

<p>
  
![Screenshot 2025-02-03 164904](https://github.com/user-attachments/assets/49988b4e-b792-4342-9676-a304b63e0773)

![Screenshot 2025-02-03 164944](https://github.com/user-attachments/assets/2a9bb396-811e-43d5-91b8-79ad6fee5be7)

![Screenshot 2025-02-03 165037](https://github.com/user-attachments/assets/231ece35-193b-4d1d-adf3-275449d15419)

![Screenshot 2025-02-03 165126](https://github.com/user-attachments/assets/926e3559-a98c-4c39-8248-b31860fdbaf2)

</p>
<p>
In the editor, go to Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies> Account Lockout Policy. 
</p>
<br />

<p>
  
![Screenshot 2025-02-03 165151](https://github.com/user-attachments/assets/0de70138-513f-4151-a69a-fcd0257805fe)

![Screenshot 2025-02-03 165347](https://github.com/user-attachments/assets/38e569ef-f518-4af6-931b-da87b9af06a9)

![Screenshot 2025-02-03 165416](https://github.com/user-attachments/assets/dd9686e1-cacc-4211-ae62-e9ae0fd6c02d)

![Screenshot 2025-02-03 165458](https://github.com/user-attachments/assets/c2d1fa4b-45a4-4ab8-8809-5ec1c39bbfb4)

</p>
<p>
On the right side, select Account lockout duration and set it to 30 minutes. Hit Apply and OK. You will see that the lockout threshold (5 invalid logon attempts) and reset account (10 minutes) have been automatically filled in. Enabled allow administrator account lockout.
</p>
<br />

<p>
  
![Screenshot 2025-02-03 165632](https://github.com/user-attachments/assets/148f0727-9bc4-44d7-bf6b-84a00c3b5ffc)

![Screenshot 2025-02-03 165719](https://github.com/user-attachments/assets/e1d2cb84-6a73-4690-a31f-0f106453c2af)

![Screenshot 2025-02-03 165742](https://github.com/user-attachments/assets/e2a3192c-c3eb-4134-9621-0eb8e00c9015)

</p>

<p>
Wait 90 minutes for the policy to update, or manually update it by logging in as jane_admin in client -1 VM, opening the Command Prompt, typing gpupdate/force, and then pressing Enter.
</p>
<br />

<p>
  
![Screenshot 2025-02-03 170406](https://github.com/user-attachments/assets/f779b798-0f18-4f28-a097-186d395abdb9)

![Screenshot 2025-02-03 170432](https://github.com/user-attachments/assets/ea2062e8-3851-48d9-94dd-00cce4816320)

![Screenshot 2025-02-03 170738](https://github.com/user-attachments/assets/494d0294-1b84-435d-8925-a265d33d3db8)

</p>
<p>
Log in to dc-1, pick a random user account, and attempt to log in ten times in client -1 with a lousy password until the account is locked. 
</p>
<br />

<p>
  
![Screenshot 2025-02-03 170933](https://github.com/user-attachments/assets/134f1ecb-4dde-4d24-8ef1-72e3a77b95f3)

</p>
<p>
Unlock the account by going back to dc-1 Active Directory Users and Computers and right-clicking mydomain to find the user whose account is locked. Double-click the user, go to Account, and check the box to unlock the account, then Apply. Go back to client -1 and log in as the user to see if it unlocks.
</p>
<br />

<p>
  
![Screenshot 2025-02-03 171123](https://github.com/user-attachments/assets/1c7df20a-8e4e-4545-b310-53d073f236c3)

![Screenshot 2025-02-03 171201](https://github.com/user-attachments/assets/ac6629f0-74c7-4130-bc5e-8102165edae3)

![Screenshot 2025-02-03 171244](https://github.com/user-attachments/assets/67f5446f-8cc1-4f40-bf2d-a4cf87065c1c)

![Screenshot 2025-02-03 171326](https://github.com/user-attachments/assets/6f19d32b-860b-4961-bb67-8cf60f633d08)

![Screenshot 2025-02-03 171519](https://github.com/user-attachments/assets/d26a3d23-5947-4853-9ba5-432b52e89de8)

![Screenshot 2025-02-03 171551](https://github.com/user-attachments/assets/db1757ab-11b9-48a0-9b78-3972f439fbd4)

</p>
<p>
With the same user, we will reset the password by right-clicking the user, selecting reset password, entering the new password, and then OK.
</p>
<br />

<p>
  
![Screenshot 2025-02-03 171727](https://github.com/user-attachments/assets/71914d98-9180-4a15-bfa8-833171247e54)

![Screenshot 2025-02-03 171745](https://github.com/user-attachments/assets/d0c2ec29-1e14-46b5-a3a2-dd8150d5a3e9)

</p>
<p>
Now, we will disable a user account by searching for the user, right-clicking the user name, and selecting "disable account." You will know the account is disabled when the icon is grayed out and you attempt to log in to client -1 with the user. The user will be locked out.
</p>
<br />

<p>
  
![Screenshot 2025-02-03 171727](https://github.com/user-attachments/assets/9b4372b7-ab5a-4313-bfdf-c7bad99206d1)

![Screenshot 2025-02-03 172004](https://github.com/user-attachments/assets/855ea3ab-a540-4bca-bbc8-d144b6ba6258)

![Screenshot 2025-02-03 172032](https://github.com/user-attachments/assets/6d31fa7c-bc47-4201-8fbb-0183688e8363)

![Screenshot 2025-02-03 172152](https://github.com/user-attachments/assets/2869de56-fa8d-4e8f-8ace-a58392ac89d9)

</p>
<p>
We will now enable the user account by returning to dc-1, finding the user in the active directory, right-clicking the user name, and selecting enable—login in client- 1 as user to check if the user can log on. 
</p>
<br />

<p>
  
![Screenshot 2025-02-03 171727](https://github.com/user-attachments/assets/f974dded-cb06-4bf6-a0c8-7bcd8939e5e8)

![Screenshot 2025-02-03 172237](https://github.com/user-attachments/assets/a15ccc77-5804-44e1-853d-a6eaeb5ca683)

![Screenshot 2025-02-03 172303](https://github.com/user-attachments/assets/0c496840-41ba-4718-87b4-490ccf61db79)

</p>
<p>
Let’s log in to dc-1 to observe the logs in the start menu type in eventwr.msc. Expand Windows Logs, select Security, and right-click Find the user previously locked out of their account. If we don’t see the failed login attempt, check the client -1 VM in Start type in eventwr.msc., but run as administrator. Used mydomain.com\jane_admin. Follow the same procedure we did for the dc-1 VM for observing the logs. You will see the Aduit Failure. 
</p>
<br />

<p>
  
![Screenshot 2025-02-03 173437](https://github.com/user-attachments/assets/07d2449b-d678-4783-8072-aa5b47b0ec9b)

![Screenshot 2025-02-03 173519](https://github.com/user-attachments/assets/45602c37-484a-45eb-965b-6a1a89040aca)

![Screenshot 2025-02-03 173540](https://github.com/user-attachments/assets/0021751b-f1b9-466a-8932-bc33d320d659)

![Screenshot 2025-02-03 173624](https://github.com/user-attachments/assets/9a30c18a-aa09-4982-8628-74964325e962)

![Screenshot 2025-02-03 173649](https://github.com/user-attachments/assets/da7c35a1-98b7-499c-b25c-8d9fc0602c60)

![Screenshot 2025-02-03 173818](https://github.com/user-attachments/assets/fcb5e52e-5664-47b0-813e-aedc32ae33cb)

![Screenshot 2025-02-03 174058](https://github.com/user-attachments/assets/ee8a0b33-3e99-4f24-a2da-1d28638bc6e2)

![Screenshot 2025-02-03 174123](https://github.com/user-attachments/assets/962f6e9b-6a55-4ab7-b15e-81e6fcd920ca)

![Screenshot 2025-02-03 174215](https://github.com/user-attachments/assets/da6027e0-86bc-45b5-86fa-cf7d17d2b67a)

![Screenshot 2025-02-03 174321](https://github.com/user-attachments/assets/7e0e6bd9-958f-485f-b33f-8affb1dc948b)

![Screenshot 2025-02-03 174526](https://github.com/user-attachments/assets/1e60466e-4f29-4360-8b73-ebfd3d90b3fd)

</p>













