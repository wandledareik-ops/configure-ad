<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Using VMs within Azure to Set up a Domain with a Domain Controller and using Active Directory</h1>
Walkthrough of Setting up a Domain, Domain Controller, and added a second VM to the Domain.  <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2025 Datacenter Azure edition
- Windows 11 Enterprise N LTSC 2024

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1- Install Active Directory Domain Services within the domain controller
- Step 2- Create Organizational Units and Admins within Active Directory
- Step 3- Add another VM to the Domain
- Step 4- Verify Client 1 is apart of the Domain 

<h2>Deployment and Configuration Steps</h2>

<p>
<img width="1458" height="757" alt="picture 1" src="https://github.com/user-attachments/assets/2e04759d-4541-4f76-a3c4-acc45fd077c8" />
</p>
<p>
First on the Domain Controller VM you open Server Manager from the start menu and click Add roles and features to install the Active Directory Services.
</p>
<br />
<img width="1781" height="766" alt="picture 2" src="https://github.com/user-attachments/assets/e1561c20-61f8-45ec-895a-df1ef0279539" />
<p>

</p>
<p>
Click next thru the menu to select the computer as the domain controller and finish the installation of the Active Directory program.
</p>
<br />

<p>
<img width="1432" height="744" alt="picture 3" src="https://github.com/user-attachments/assets/faca911b-8f8c-48bb-ad0c-71b0d74a4cb8" />
</p>
<p>
This shows DC-1 is the domain controller for the mydomain.com domain name. This computer is will also be the DNS server for itself and any other computer that gets added to the domain.
</p>
<br />

<img width="776" height="546" alt="picture 5" src="https://github.com/user-attachments/assets/eed30dcb-70f4-47b7-8808-f8f9bc003343" />

</p>
<br />
First, we create an Organizational Unit within Active Directory so we can organize our organization. To do this we open Active Directory by selecting start and searching for Active Directory Users and Computers. Then we right click mydomain.com then click new, Organization Unit and name it Admins    

<p>
<img width="774" height="544" alt="picture 4" src="https://github.com/user-attachments/assets/5a676a61-10bf-4bf6-8be5-77a9b6f8f294" />

 
</p>
<br />
Next, we create a Domain Admin that will be able to make changes within Active Directory. Open the new Admins OU and right click the blank space and select new and select users. Fill out the info and finish the process.

<p>
<img width="779" height="542" alt="picture 6" src="https://github.com/user-attachments/assets/b24c4e48-0d7b-480f-88d9-8531ea44f1e5" />
</p>
<br />
To make a user into a Domain Admin we right click the user then click properties then up top we select member of then add. Search for Domain Admins then apply and ok.
<p>
 <img width="760" height="536" alt="picture 7" src="https://github.com/user-attachments/assets/90a10753-0a4f-4d69-bcd7-7a987301d654" />

</p>
<br />
We can move the users into different OUs to keep everything straight. Here we can see the new User within the Admin OU.

<p>
<img width="1152" height="619" alt="picture 8" src="https://github.com/user-attachments/assets/57717f95-c8f6-4ce2-afa9-df0d5ca538c4" />
 
</p>
<br />
Now we want to add another computer into the domain. First, we need to make sure that the client computer is configured to use the Domain Controller as it's DNS server. For our project we can set this within Azure. Within Azure is navigate to the VM and go to Settings then DNS servers and select Custom and put in the private IP address of our Domain Controller. 
<p>
 <img width="471" height="289" alt="picture 9" src="https://github.com/user-attachments/assets/f80909dc-5b07-47e9-8c37-a6b2c74bcce0" />

</p>
<br />
We then take the public IP address of our Client VM and with Remote Desktop Connections we can connect to the VM. To do this we search for the Remote Desktop Connection within the start menu.

<p>
<img width="1226" height="944" alt="picture 10" src="https://github.com/user-attachments/assets/916c6f63-d254-44c8-89bc-cce6733874f5" />
 
</p>
<br />
Log in to Client VM as the original User and open the System settings. Scroll down to About then click Domain or workgroup. A domain option will be available, and you type in the name of the domain you wish to add the VM too. Making sure nothing is mispelled. 
<p>
<img width="771" height="540" alt="picture 11" src="https://github.com/user-attachments/assets/41f80027-8134-4cb5-a710-74af279f78b6" />

</p>
<br />
If done correctly we can go back to the Domain Controller and open Active Directory. It will by default be in the Computers OU, but you can move it elsewhere. I created the _CLIENTS OU and put it there. 

