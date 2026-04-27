<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Azure Active Directory Setup</h1>
This lab builds on the previous exercise in which I installed Active Directory and set up a domain controller. In this lab, I will configure Active Directory, join a client machine to the domain, and create user accounts. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure
- Active Directory
- PowerShell
- Remote Desktop

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 Pro 

<h2>Setup Steps</h2>

<p>
<img width="1702" height="924" alt="image" src="https://github.com/user-attachments/assets/8bb342f2-d626-4a6e-9aea-be89d2432585" />
<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/f5df4854-ca0e-44bf-9f0c-23b56c2be4f7" />

</p>
<p>
Now that Active Directory has been installed on the domain controller virtual machine, the next step is to create Organizational Units (OUs) and user accounts. Using the Active Directory Users and Computers console, right-click on the domain you created (in this case, ernestotest.com) and create a new Organizational Unit. I created two OUs: _EMPLOYEES and _ADMINS. This naming convention is intentional, as it will be used later in a PowerShell script. Within the _ADMINS OU, I created a new user named Jane Doe. Her account is assigned administrative privileges through a security group. To grant these permissions, right-click the user, open Properties, navigate to the Member Of tab, and add the appropriate security group. In this case, Jane was added to the Domain Admins group. Going forward, all administrative tasks will be performed using Jane’s account. I will log out of the labuser account and sign in as jane_admin.
</p>
<br />

<p>
<img width="3490" height="1638" alt="image" src="https://github.com/user-attachments/assets/d150c717-0f12-415e-8c16-62a5181d51a5" />

</p>
<p>
Before a client machine can join the domain, the DNS settings must be configured correctly. The DNS server should point to the domain controller’s private IP address. In the Azure portal, navigate to the Networking tab and select the Network Interface. Under the DNS settings, enter the private IP address of the domain controller and save the changes. Finally, restart the client virtual machine to ensure the new DNS configuration is applied.
</p>
<br />

<p>
<img width="1763" height="892" alt="image" src="https://github.com/user-attachments/assets/93b8974a-bcea-445b-9969-0bd3f5894f5b" />

<img width="1702" height="924" alt="image" src="https://github.com/user-attachments/assets/39e52225-3069-4b18-97e9-3571e2f2d7b2" />

<img width="1713" height="918" alt="image" src="https://github.com/user-attachments/assets/e2bd8605-ea9b-4bd2-9bec-71779cdf4261" />

</p>
<p>
The next step is to join the client virtual machine to the domain. On the client VM, open the System settings, select Rename this PC (advanced), and click Change. Enter the domain name along with the required credentials to complete the domain join process. For this lab, I am using the Jane Doe account. Be sure to enter the login credentials in the proper domain format. Once completed, the client machine should successfully join the domain. On the domain controller, the client will appear under the Computers container in the Active Directory Users and Computers console.
</p>
<br />

<p>
<img width="1749" height="899" alt="image" src="https://github.com/user-attachments/assets/6c3c2abe-3e24-454c-bbdf-3640e93688fc" />

</p>
<p>
Before domain users can access the client computer, Remote Desktop must be enabled for non-administrative accounts. While logged in as an administrator (in this case, Jane), open System Properties, navigate to the Remote Desktop tab, and select Users that can remotely access this PC. Add the Domain Users group to grant them Remote Desktop access. With this configuration in place, non-administrative users can now log in to Client-1. In a typical environment, this type of setting would be managed through Group Policy to apply changes across multiple systems. However, for this lab, the configuration is being done manually instead.



  
</p>
<br />

<p>
<img width="3252" height="1732" alt="image" src="https://github.com/user-attachments/assets/00833c20-947e-420b-9efa-470bb3eb574f" />

<img width="1298" height="740" alt="image" src="https://github.com/user-attachments/assets/078581dc-1574-4957-8a4f-97e3bc219895" />

</p>
<p>



User accounts can be created either manually or by using automation. For this lab, I will be using a PowerShell script. The script is available at the provided <a href="https://github.com/AsiaPonder001/BunchofUsers/blob/main/README.md?plain=1)"> GitHub link. </a> The script is available at the provided GitHub link.On the domain controller, open PowerShell ISE with administrative privileges, ensuring you are logged in with a domain administrator account. Create a new file in the ISE, paste the script into the console, and execute it. Once the script runs, you can observe the user accounts being generated automatically.
</p>
<br />

<p>
<img width="1753" height="897" alt="image" src="https://github.com/user-attachments/assets/4e7e90af-d79d-4e6c-9358-098208d3b1de" />

</p>
<p>
After the user accounts have been created, Client-1 can now be accessed using one of the newly generated users from the PowerShell script. Select a user and sign in to the client machine using the appropriate domain credentials. In my case, I logged in with shafeentest.com\bon.rovej.
</p>
<br />

<h2>Lessons Learned</h2>

Completing this lab helped me understand how to set up Active Directory and join client machines to a domain. I also gained experience creating user accounts and assigning the appropriate permissions. While navigating the various menus can be a bit involved, Active Directory itself is not overly difficult to learn.This lab also serves as a foundation for exploring DNS configuration in greater detail, as well as understanding file permissions in practice. I plan to cover these topics more thoroughly in future labs.
