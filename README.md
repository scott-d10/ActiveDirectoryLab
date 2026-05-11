# Active Directory Installation and Configuration Home Lab

## Overview
This home lab was built using Windows Server 2025 and VMware Workstation to demonstrate core Active Directory administration skills, including:

- Active Directory installation
- Organisational Units
- User and group management
- Group Policy Objects
- Remote Desktop configuration
- Security policy management

## Tools Used
- Windows Server 2025
- Windows 11
- VMware Workstation
- Active Directory Users and Computers
- Group Policy Management

## Lab Objectives
- Create a domain
- Build an Organisational structure
- Create users and groups
- Apply Group Policys

## Walkthrough

### 1. Installing and Configuring Active Directory
From the Windows Server menu, I clicked Manage and selected Add Roles and Features.  I then selected Role-based or feature-based installation and selected my server on the following page.  This then brought me to the xx page where I was able to select Active Directory Domain Services for installation.

![Installing Active Directory](https://i.ibb.co/TMM405yf/Installing-Active-Directory.png)
<br>
<br>
<br>
As there is no active domain controller, once Active Directory Domain Services installed successfully I selected the link to Promote this server to a domain controller.  This then brought me to the Deployment Configuration where I selected Add a new forest and named the Root domain example.local.  

![Configuring the Domain](https://i.ibb.co/DDwyx34z/Domain-Configuration.png)
<br>
<br>
<br>
Once settings up the domain, Server Manager initiated a Prerequisite Check – this was successful.  I then clicked to install.

![Prerequisite Check](https://i.ibb.co/xKyZ2Vr4/Prerequisite-Check.png)

---

### 2. Creating Organisational Units
To create these, from the drop down menu Tools within Server Manager I selected Active Directory Users and Computers.  From here I right clicked on the example.local domain, selected new, then Organisational Unit.

![Creation Path](https://i.ibb.co/tTPJKsP0/OU-Filepath.png)
<br>
<br>
<br>
For this lab, I created three Organisational Units:<br>
  ***Accounting*** <br>
  ***HR***<br>
  ***Sales***

![Final OU’s](https://i.ibb.co/QhFJjqz/Completed-OUs.png)

---

### 3. Creating Users and Groups
Now that the Organisational Units have been created, the groups and users within these can be added.  Firstly, I created three groups for the corresponding Organisational Units:<br>
***Accounting_Users***<br>
***HR_Users***<br>
***Sales_Users***<br>
<br>
I did this by right clicking the Organisational Unit down the left hand side, selecting New then Group.

![Adding a Group](https://i.ibb.co/FqBjf7qv/Creating-a-Group.png)
<br>
<br>
<br>
Once these groups were created, I then added a user into each Organisational Unit:<br>
***Angela Smith for Accounting***<br>
***Harry Jones for HR***<br>
***Simon White for Sales***

![Adding a User](https://i.ibb.co/Z6KFv79K/Creating-User.png)
<br>
<br>
<br>
Now both users and groups have been created within the Organisational Units, I can add the users into these groups and prepare to create and apply appropriate Group Policy Objects for each department.  I did this by double clicking the Group within the Organisational Unit, selecting the Members tab across the top, clicking add and typing their name into the box, clicking Check Names to confirm it was correct, then clicking ok.

![Adding User to a Group](https://i.ibb.co/LD2nRnmr/Adding-User-to-Group.png)

---

### 4. Applying Group Policy
I then created and applied the following Group Policy Objects for each department:<br>
***Accounting – restrict removeable storage***<br>
***HR – password and screenlock***<br>
***Sales – RDP access***

To create the Group Policies, from the drop down menu, Tools, within Server Manager I selected Group Policy Management.  I then expanded Forest: example.local, Domains and finally examples.local.  Within here are the three Organisational Units I previously created along with their corresponding Groups and Users.  I then right clicked on the Organisational Unit, selected ‘Create a GPO in this domain, and Link it here’ and named it appropriately.  

![Creating and Naming a GPO](https://i.ibb.co/MxkPzZPn/GPO-creation.png)
<br>
<br>
<br>
To improve endpoint security, I configured a Group Policy to automatically lock inactive HR workstations.  To do this, once the policy was created, I right clicked and selected ‘Edit’ to open the Group Policy Management Editor.  I navigated to User Configuration, Policies, Administrative Templates, Control Panel then Personalisation.  From here I configured ‘Enable Screen Saver’, ‘Password Protect the Screen Saver’ and ‘Screen Saver Timeout’ to Enable.

![HR GPO](https://i.ibb.co/0yTtRNtT/HR-GPO-s-Enabled.png)
<br>
<br>
<br>
To reduce the risk of unauthorised data transfer, I configured a Group Policy to restrict removable storage access for Accounting users.  To do this, within the Group Policy Management Editor, I navigated to Computer Configuration, Policies, Administrative Templates, System then Removable Storage Access.  From here I configured ‘All Removable Storage Classes: Deny all access’ to Enable.

![Accounting GPO](https://i.ibb.co/7P4q9DP/Accounting-GPO-s-Enabled.png)
<br>
<br>
<br>
To give the sales staff the ability to work remotely, I created a Group Policy that would allow them to log on using RDP.  To do this, within the Group Policy Management Editor, I navigated to Computer Configuration, Policies, Administrative Templates, Windows Components, Remote Desktop Services, Remote Desktop Session Host then Connections.  I then configured ‘Allow users to connect remotely using Remote Desktop Services’ to Enable.  

![Sales GPO](https://i.ibb.co/Q34tb1T8/Sales-GPO-s-Enabled.png)
<br>
<br>
<br>
Once the Group Policy Objects had been implemented, it was important to run the PowerShell command ‘gpupdate /force’ on the client machines so the policies were applied to the users.

---

## Summary and Skills Learned
This lab helped strengthen my understanding of Active Directory administration, organisational unit structure, group policy management and user access control within a Windows Server environment.<br>
### Skills Demonstrated:

- Active Directory Administration
- Group Policy Management
- Windows Server 2025
- VMware Workstation
- User & Group Management
- Organisational Unit Structuring
- Remote Desktop Configuration
- Basic Endpoint Security
