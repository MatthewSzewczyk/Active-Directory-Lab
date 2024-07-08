<h1>Active Directory Home Lab</h1>



<h2>Description</h2>
For this project, I established a Windows domain accommodating 1000 users. I employed a Windows Server 2022 virtual machine as the Domain Controller, alongside a Windows 10 Enterprise virtual machine configured to connect to this DC. The setup process included configuring network adapters, assigning IP addresses, installing Active Directory Services, and creating domain accounts. To streamline user creation, I automated the process using a PowerShell script. Finally, I integrated and configured the Windows 10 VM to join the domain.
<br />


<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b> 
- <b>Active Directory</b>

<h2>Environments Used </h2>

- <b>Windows 10 Enterprise</b>
- <b>Windows Server 2022</b>

<h2>Project walk-through:</h2>

<p align="center">
Started by creating windows server 2022 Virtual Machine (VM) in virtual box, dedicating the appropriate ram, CPU cores, and dedicated storage to the VM: <br/>
<img src="https://i.imgur.com/9OWfdk9.png" height="80%" width="90%" alt="AD project"/>
<br />
<br />
Starting VM and completing windows server installation process, choosing a custom installation to format server from scratch:  <br/>
<img src="https://i.imgur.com/kQlfMp2.png" height="80%" width="90%" alt="AD project"/>
<img src="https://i.imgur.com/GNtEYwf.png" height="80%" width="90%" alt="AD project"/>
<br />
<br />
Once loaded in I set up the internal NIC with the following, excluding the Gateway because the Domain Controller (DC) will serve as the default Gateway since its connected to the external NIC which will get the addressing from my physical router. The DNS server will be given its loop back address to use the DC as the DNS server: <br/>
<img src="https://i.imgur.com/yvGnYKR.png" height="80%" width="90%" alt="AD project"/>
<img src="https://i.imgur.com/7yFV9A5.png" height="80%" width="90%" alt="AD project"/>
<br />
<br />
Next I installed Active Directory Domain Services via the manage drop down in the top right of the server manager dashboard:  <br/>
<img src="https://i.imgur.com/6bt9mU9.png" height="90%" width="90%" alt="AD project"/>
<br />
<br />
After installation I completed the post deployment configurations for the DC which was opened through the flag symbol located at the top left of the dashboard. After opening the deployment configurations menu I added a new forest called Mattsdomain.com and created a password. Thus, finishing the AD domain services installation:  <br/>
<img src="https://i.imgur.com/uZiqrXy.png" height="80%" width="90%" alt="AD project"/>
<br />
<br />
Next I created a new Organizational Unit (OU) called _ADMIN in the AD user and computers and then created a user within that OU to be used as the DC admin account:  <br/>
<img src="https://i.imgur.com/1kiL16x.png" height="80%" width="90%" alt="AD project"/>
<img src="https://i.imgur.com/Xf2L2sS.png" height="80%" width="90%" alt="AD project"/>
<img src="https://i.imgur.com/hvgJbl3.png" height="80%" width="90%" alt="AD project"/>
<br />
<br />
I then added the DC admin account as a member of domain admins group by right clicking the name, selecting properties, and moving into the Member Of tab:  <br/>
<img src="https://i.imgur.com/QAUH6xs.png" height="80%" width="90%" alt="AD project"/>
<br />
After finalizing the account I logged out and then signed into the admin account:  <br/>
<img src="https://i.imgur.com/H1EMqQT.png" height="80%" width="90%" alt="AD project"/>
<br />
<br />
Next I installed Remote Access role through the Add Roles and Feature located in the Server Managers dashboard, checking off Routing in Role Services tab before initializing the install:  <br/>
<img src="https://i.imgur.com/Sg0W7Re.png" height="80%" width="90%" alt="AD project"/>
<img src="https://i.imgur.com/UgwB6Q1.png" height="80%" width="90%" alt="AD project"/>
<br />
<br />
After Remote Access was installed, I then configured the NAT through Tools > Routing and Remote Access within the dashboard:  <br/>
<img src="https://i.imgur.com/VK6d5YT.png" height="80%" width="90%" alt="AD project"/>
<br />
<br />
Next I installed a DHCP Server on the DC:  <br/>
<img src="https://i.imgur.com/ATHaBIO.png" height="80%" width="90%" alt="AD project"/>
<br />
<br />
After installation I then configured a new Scope for the DHCP Server through Tools > DHCP > IPv4. Creating the start and end IP addresses for the network and the lease times for the IP addresses:  <br/>
<img src="https://i.imgur.com/mklNIGa.png" height="80%" width="90%" alt="AD project"/>
<br />
<br />
Before completing the scope I set the default gateway as the DC IP address. Allowing users on the domain to connect to the internet through the DC:  <br/>
<img src="https://i.imgur.com/0ELD9ac.png" height="80%" width="90%" alt="AD project"/>
<br />
<br />
I then ran a PowerShell script that will create 1000 users with names stored in a notes document:  <br/>
<img src="https://i.imgur.com/EUYwWkt.png" height="80%" width="90%" alt="AD project"/>
<br />
<br />
This is a basic for loop script that automates the process of creating a new user in the Active Directory Users and Computers tab. Filling out all the necessary information needed during the process like name, username, password, and directory of where the user will be stored (Area filled out by PowerShell Shown below):  <br/>
<img src="https://i.imgur.com/NXelhFZ.png" height="80%" width="90%" alt="AD project"/>
<br />
<br />
Once users were done I then Downloaded and installed Windows 10 Enterprise. Before launching the VM I set the network adapter to attach to the internal network Lan 0 which will connect the Windows 10 VM to the DC which then connects to the internet:  <br/>
<img src="https://i.imgur.com/XM1jPYm.png" height="80%" width="80%" alt="AD project"/>
<br />
<br />
After installing the Windows 10 VM I renamed the computer name and joined the domain:  <br/>
<img src="https://i.imgur.com/EzMEesx.png" height="80%" width="90%" alt="AD project"/>
<br />
<br />
Finally I checked the IP configurations on the Windows 10 VM to make sure they were correct, pinged google to make sure internet connectivity was working, and signed into multiple user accounts to confirm all user were able to log into the domain. Thus completing my objective of creating a fully functioning domain with Active Directory service:  <br/>
<img src="https://i.imgur.com/7gVK9nY.png" height="80%" width="90%" alt="AD project"/>
<br />
</p>

