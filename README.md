<p align="center">
<img src="https://i.imgur.com/aMMGyHQ.jpeg" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />

<h1>Deploying Active Directory in Azure</h1>



<h2>Description</h2>
In this part of the Active Directory project, we will install Active Directory on the domain controller, create a domain admin account, and join the client VM to the domain.<br/>
<br />

<h2>Environments and Utilities Used</h2>

- <b>Microsoft Azure</b>
- <b>Virtual Machines</b>
- <b>Remote Desktop Connection</b>
- <b>Active Directory</b>

<h2>Operating Systems Used </h2>

- <b>Windows Server </b>
- <b>Windows 10</b>

<h2>Project Walkthrough:</h2>

<p align="center">
To begin, open the Server Manager dashboard on the Domain Controller (DC) if it isn't already displayed.<br/>

  
  ![image](https://github.com/user-attachments/assets/f90a79dd-8570-4022-ae47-b291ed29888b)


Here, click on Add roles and features, then click Next twice. For server selection, there should be only one option available to choose from: br/>

![image](https://github.com/user-attachments/assets/2e2abf52-7fd2-4d85-b2d8-c12f5d077ca7)



Now, check "Active Directory Domain Services" > Click "Add Features":  <br/>



![image](https://github.com/user-attachments/assets/ea2282c9-d42e-4c15-9619-c141c815e8c2)



 Select Active Directory Domain Services, then click Next three times. Now check the box for Restart the destination server automatically if required, and click Install. br/>



![image](https://github.com/user-attachments/assets/b0948068-ba35-4383-b69a-c07604134b3b)







Next, you need to promote this machine to a Domain Controller by configuring it as a new forest with the name "mydomain.com" (you can choose any name; "mydomain.com" is just easy to remember). To do this, click on the flag icon with the caution symbol near the top-right corner of the Server Manager Dashboard and select Promote this server to a domain controller.<br/>




![image](https://github.com/user-attachments/assets/16bec3ab-6bd9-43aa-b048-817afea9ee99)




 Then, choose Add a new forest and enter "mydomain.com" in the Root domain name field. After that, click Next.






![image](https://github.com/user-attachments/assets/8758393b-3b27-4d41-a682-6e794166f78e)





Type in a password of your choosing on the next screen like so then hit "Next":  


![image](https://github.com/user-attachments/assets/28aa93d1-d223-4935-93d2-ebb4b8d07e6d)

Leave the Create DNS delegation option unchecked and click Next. Continue clicking Next until you reach the installation screen. On this screen, click Install. The machine will restart once the installation is complete.<br/>



![image](https://github.com/user-attachments/assets/77b403a1-29b4-4d0f-b886-c9f043232518)



![image](https://github.com/user-attachments/assets/06b7ce49-ea03-4cdb-aa03-45f9cd3c9d11)





It may take some time for the machine to restart, but once it's back up, sign in using "mydomain.com\labuser" (if you're using the same naming conventions as I am) as the username. Enter the password you set for "labuser." You need to sign in as "mydomain.com\labuser" rather than just "labuser" because you have promoted this machine to a Domain Controller, and it must identify the context of the user logging in (whether they are a domain user or a local user). To sign in as a user on the domain, you specify this with the "mydomain.com" prefix during the login process.

![image](https://github.com/user-attachments/assets/06131a3b-65d8-4b65-bf2f-601b111d5636)





  Now, you will create an admin user. To do this, type "Active Directory Users and Computers" into the Start search bar.



![image](https://github.com/user-attachments/assets/b9707b6a-c1d4-40f6-988e-de9f07c4ce69)



Right-click on "mydomain.com" and select New > Organizational Unit. Name it exactly "_EMPLOYEES" (you will use this name in a future project that involves running a script). Repeat these steps to create another OU (Organizational Unit) named "_ADMINS."



![image](https://github.com/user-attachments/assets/0ccdc5d7-4fe2-4a36-8294-55f51baca320)



Next, create a new user in "_ADMINS" by right-clicking on "_ADMINS" > New > User and fill it out like so:  <br/>





![image](https://github.com/user-attachments/assets/0a2ed839-2aa9-446b-a424-ad7074dab3dd)


![image](https://github.com/user-attachments/assets/88d90fa9-c6bf-412a-a901-47d75f7c8836)






Next, create a password, uncheck User must change password at next logon, and check Password never expires.<br/>


![image](https://github.com/user-attachments/assets/1cc8c237-d1ed-4060-bb38-e749a765c8eb)




Jane Doe is now a member of the "_ADMINS" OU, but she isn’t actually an admin yet. To grant her admin privileges, right-click on her name, select Properties, go to the Member Of tab, click Add..., enter "domain admins," click Check Names, then OK. Finally, click Apply and then OK.

![image](https://github.com/user-attachments/assets/25529a18-c2d4-4a1e-874c-eff203cd07e4)





Now, you can log out of DC and log back in using Jane's credentials:  <br/>


![image](https://github.com/user-attachments/assets/98322885-6b85-449a-ba70-3f1b1693ef62)



Once logged in, access the client-1 VM if you aren't already on it. Here, you will join this client to the domain by right-clicking the Start menu, selecting System, then Rename this PC (advanced). Next, click Change, select Domain, enter "mydomain.com," and hit OK.<br/>



![image](https://github.com/user-attachments/assets/6c5c3216-cf2e-4b1f-b71d-b9b9b1cb7ffc)




  

After the restart, client-1 is now a member of the domain. To check, in the DC machine start seach bar, search for "Active Directory Users and Computers" > mydomain.com > Computers > client-1 should be listed:  <br/>


![image](https://github.com/user-attachments/assets/56f5e604-a9a0-434e-8caa-4db5cab5ad48)


  Now, you can create another OU just like before and name it "_CLIENTS." Then, drag and drop client-1 from the "Computers" section into "_CLIENTS."br/>



![image](https://github.com/user-attachments/assets/a8e8c7bb-fd00-4e6b-a906-fa1c745ae3c7)





  


<h2>Active Directory is Deployed and Ready for Use! </h2>
