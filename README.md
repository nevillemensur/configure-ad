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

<h2>High-Level Deployment and Configuration Steps</h2>

Setup Resources in Azure

1. Create the Domain Controller VM (Windows Server 2022) named “DC-1”
Take note of the Resource Group and Virtual Network (Vnet) that get created at this time

2. Create the Client VM (Windows 10) named “Client-1”. Use the same Resource Group and Vnet that was created in Step 1.

3. Set Domain Controller’s NIC Private IP address to be static

4. Ensure that both VMs are in the same Vnet (you can check the topology with Network Watcher


Ensure Connectivity between the client and Domain Controller

5. Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping -t <ip address> (perpetual ping)
  
6. Login to the Domain Controller and enable ICMPv4 in on the local windows Firewall
  
7. Check back at Client-1 to see the ping succeed


Install Active Directory
  
8. Login to DC-1 and install Active Directory Domain Services
  
9. Promote as a DC: Setup a new forest as mydomain.com (can be anything, just remember what it is)
  
10. Restart and then log back into DC-1 as user: mydomain.com\labuser
  

Create an Admin and Normal User Account in AD
  
11. In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”
  
12. Create a new OU named “_ADMINS”
  
13. Create a new employee named “Jane Doe” (same password) with the username of “jane_admin”
  
14. Add jane_admin to the “Domain Admins” Security Group
  
15. Log out/close the Remote Desktop connection to DC-1 and log back in as “mydomain.com\jane_admin”
  
16. User jane_admin as your admin account from now on


Join Client-1 to your domain (mydomain.com)
  
  
17. From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address
  
18. From the Azure Portal, restart Client-1
  
19. Login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain (computer will restart)
  
20. Login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers (ADUC) inside the “Computers” container on the root of the domain
  


Setup Remote Desktop for non-administrative users on Client-1
  
21. Log into Client-1 as mydomain.com\jane_admin and open system properties
  
22. Click “Remote Desktop”
  
23. Allow “domain users” access to remote desktop
  
24. You can now log into Client-1 as a normal, non-administrative user now
  

Create a bunch of additional users and attempt to log into client-1 with one of the users
  
25. Login to DC-1 as jane_admin
  
26. Open PowerShell_ise as an administrator
  
27. Create a new File and paste the contents of the script into it
  
28. Run the script and observe the accounts being created
  
29. When finished, open ADUC and observe the accounts in the appropriate OU
  
30. Attempt to log into Client-1 with one of the accounts (take note of the password in the script)

<h2>Deployment and Configuration Steps</h2>

<p>
1. Create the Domain Controller VM (Windows Server 2022) named “DC-1”
Take note of the Resource Group and Virtual Network (Vnet) that get created at this time
</p>
<p>
<img src="https://i.imgur.com/aLD1hnh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/poDExMi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>  
</p>
<br />
  
<p>
2. Create the Client VM (Windows 10) named “Client-1”. Use the same Resource Group and Vnet that was created in Step 1.
</p>
<p>
<img src="https://i.imgur.com/552iIki.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/HC947jT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>  
</p>
<br />
  
<p>
3. Set Domain Controller’s NIC Private IP address to be static
</p>  
<p>
<img src="https://i.imgur.com/Iqm1DfO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/AgH2Muv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/myo3PGA.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/uHz8DyB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/0wA98F8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
4. Ensure that both VMs are in the same Vnet 
</p>
<p>
<img src="https://i.imgur.com/kH5VlBM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/H8sVUPb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
<br />
  
<p>
Ensure Connectivity between the client and Domain Controller
 
5. Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping -t <ip address> (perpetual ping)
</p>
<p>
<img src="https://i.imgur.com/LTdaQuF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
6. Login to the Domain Controller and enable ICMPv4 in on the local windows Firewall
</p>  
<p>
<img src="https://i.imgur.com/ExlrAka.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/PxQIZZR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/8Gg67nz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/KoIiIcH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>
7. Check back at Client-1 to see the ping succeed
</p>
<img src="https://i.imgur.com/Tym9abj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
  
<p>
Install Active Directory

8. Login to DC-1 and install Active Directory Domain Services
</p>
<p>
<img src="https://i.imgur.com/y18ylMT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DOYedn0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/FOCwaur.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/qvyiwss.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/tlIfTYg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/qvyiwss.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/cKEzuKT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/e1FaNTE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/cUfqOuL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>
9. Promote as a DC: Setup a new forest as mydomain.com (can be anything, just remember what it is)
</p>
<img src="https://i.imgur.com/Iq8UBZY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/dzmbPq0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/3ixR49M.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/znEIGvB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>
10. Restart and then log back into DC-1 as user: mydomain.com\labuser
</p>
<img src="https://i.imgur.com/dBxUSV0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
  
<p>
Create an Admin and Normal User Account in AD
  
11. In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”
</p>
<p>
<img src="https://i.imgur.com/cSFuAQF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/ZfdX6qQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/Fd9kxLj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
  
<p>
12. Create a new OU named “_ADMINS”
</p>
<p>
<img src="https://i.imgur.com/ZfdX6qQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/zuOSYNt.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
  
<p>
13. Create a new employee named “Jane Doe” (same password) with the username of “jane_admin”
</p>
<p>
<img src="https://i.imgur.com/pWJgqmy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/hwtCmYT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/eGog1Pg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
  
<p>
14. Add jane_admin to the “Domain Admins” Security Group
</p>
<p>
<img src="https://i.imgur.com/SDA2UUB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/UfFZpPo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/n6y3qNr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/Xsp577O.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/GxzmLyL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/FkbTbDA.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/s4A7waW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
15. Log out/close the Remote Desktop connection to DC-1 and log back in as “mydomain.com\jane_admin”
</p>
<p>
<img src="https://i.imgur.com/sXrBEFM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DOGsz7W.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
16. User jane_admin as your admin account from now on
</p>
<p>
<img src="https://i.imgur.com/eEwmSr0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
  
<p>
17. Join Client-1 to your domain (mydomain.com)

From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address
</p>
<p>
<img src="https://i.imgur.com/HohTX1z.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/dtEGmcp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/FDPLiOv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/4gPk3Gi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
  
<p>
18. From the Azure Portal, restart Client-1
</p>
<p>
<img src="https://i.imgur.com/F4t3nmp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
19. Login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain (computer will restart)
</p> 
<p>
<img src="https://i.imgur.com/GyTjVHO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/nA5VrTq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/rlrVZFJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/AwIQOkc.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  
<p>
20. Login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers (ADUC) inside the “Computers” container on the root of the domain
</p>
<img src="https://i.imgur.com/Ude5Ol1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/bbdwxB0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
  
<p>
Setup Remote Desktop for non-administrative users on Client-1
  
21. Log into Client-1 as mydomain.com\jane_admin and open system properties
</p>

<p>
<img src="https://i.imgur.com/ZXBsZyV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/V7IgETU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<p>
22. Click “Remote Desktop”
</p>
<img src="https://i.imgur.com/QzJqofX.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<p>
23. Allow “domain users” access to remote desktop
</p>

<img src="https://i.imgur.com/ty1kykP.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/SF1VqsP.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/PKjEXbZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/R49WUfG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<p>
24. You can now log into Client-1 as a normal, non-administrative user now
</p>

<img src="https://i.imgur.com/7fr66xi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/SFV29mK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/0VRFsLi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Create a bunch of additional users and attempt to log into client-1 with one of the users
  
25. Login to DC-1 as jane_admin

</p>
  
<p>
<img src="https://i.imgur.com/bxHrznP.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
26. Open PowerShell_ise as an administrator
</p>
  
<p>
<img src="https://i.imgur.com/6GjCqex.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
27. Create a new File and paste the contents of the script into it 
</p>
  
<p>
<img src="https://i.imgur.com/4RkjuL7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/q4idPdn.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/gmwkhE2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />  

<p>
28. Run the script and observe the accounts being created
</p>

<p>
<img src="https://i.imgur.com/JxC1DoY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />  

<p>
29. When finished, open ADUC (Active Directory Users and Computers) and observe the accounts in the appropriate OU
</p>

<p>
<img src="https://i.imgur.com/ZowQJ93.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br /> 

<p>
30. Attempt to log into Client-1 with one of the accounts (take note of the password in the script)
</p>

<p>
<img src="https://i.imgur.com/AwRBw1l.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/MOyCKFn.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/fR8zni4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />  
