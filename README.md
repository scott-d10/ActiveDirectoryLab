# Active Directory Installation and Configuration Home Lab

## Overview
In this lab I will demonstrate how to utilise Windows Server to create an Active Directory Domain, build Organisational Units with users and groups and demonstrate how to apply appropriate Group Policy Objects.

## Tools Used
- Windows Server 2025
- Windows 11
- VMware Workstation
- Active Directory Users and Computers
- Group Policy Management

## Lab Objectives
- Create a domain
- Build an OU structure
- Create users and groups
- Apply Group Policys

## Walkthrough

### 1. Installing and Configuring Active Directory
From the Windows Server menu, I clicked Manage and selected Add Roles and Features.  I then selected Role-based or feature-based installation and selected my server on the following page.  This then brought me to the xx page where I was able to select Active Directory Domain Services for installation.

![Installing Active Directory](https://i.ibb.co/TMM405yf/Installing-Active-Directory.png)


As there is no active domain controller, once Active Directory Domain Services installed successfully I selected the link to Promote this server to a domain controller.  This then brought me to the Deployment Configuration where I selected Add a new forest and named the Root domain example.local.  

![Configuring the Domain](https://i.ibb.co/DDwyx34z/Domain-Configuration.png)


Once settings up the domain, Server Manager initiated a Prerequisite Check – this was successful.  I then clicked to install.

![Prerequisite Check](https://i.ibb.co/xKyZ2Vr4/Prerequisite-Check.png)


### 2. Creating Organisational Units
To create these, from the drop down menu Tools within Server Manager I selected Active Directory Users and Computers.  From here I right clicked on the example.local domain, selected new, then Organisation Unit.

![Creation Path](https://i.ibb.co/tTPJKsP0/OU-Filepath.png)


For this lab, I created three Organisational Units – Accounting, HR and Sales

![Final OU’s](https://i.ibb.co/QhFJjqz/Completed-OUs.png)


### 3. Creating Users and Groups
Now that the Organisational Units have been created, the groups and users within these can be added.  Firstly, I created three groups for the corresponding Organisation Units – HR_Users, Accounting_Users and Sales_Users.  I did this by right clicking the Organisational Unit down the left hand side, selecting New then Group.

![Adding a Group](https://i.ibb.co/FqBjf7qv/Creating-a-Group.png)


Once these groups were created, I then added a user into each Organisation Unit – Harry Jones for HR, Angela Smith for Accounting and Simon White for Sales.

![Adding a User](https://i.ibb.co/Z6KFv79K/Creating-User.png)


Now both users and groups have been created within the Organisational Units, I can add the users into these groups and prepare to create and apply appropriate Group Policy Objects for each department.  I did this by double clicking the Group within the Organisational Unit, selecting the Members tab across the top, clicking add and typing their name into the box, clicking Check Names to confirm it was correct, then clicking ok.

![Adding User to a Group](https://i.ibb.co/LD2nRnmr/Adding-User-to-Group.png)


### 4. Applying Group Policy
I then created and applied the following Group Policy Objects for each department:
- HR – Password and Screenlock policy;
- Accounting – restrict removeable storage;
- Sales – RDP access.

To create the Group Policy’s, from the drop down menu, Tools, within Server Manager I selected Group Policy Management.  I then expanded Forest: example.local, Domains and finally examples.local.  Within here are the three Organisational Units I previously created along with their corresponding Groups and Users.  I then right clicked on the Organisation Unit, selected ‘Create a GPO in this domain, and Link it here’ and named it appropriately.  

![Creating and Naming a GPO](https://i.ibb.co/MxkPzZPn/GPO-creation.png)


HR handles confidential employee information, so I chose to implement stricter session security.  To do this, once the Policy was created, I right clicked and selected ‘Edit’ to open the Group Policy Management Editor.  I navigated to User Configuration, Policies, Administrative Templates, Control Panel then Personalisation.  From here I configured ‘Enable Screen Saver’, ‘Password Protect the Screen Saver’ and ‘Screen Saver Timeout’ to Enable.

![HR GPO](https://i.ibb.co/0yTtRNtT/HR-GPO-s-Enabled.png)


Accounting deals with sensitive financial and payroll data, so blocking USB storage devices is a realistic security control.  To do this, within the Group Policy Management Editor, I navigated to Computer Configuration, Policies, Administrative Templates, System then Removable Storage Access.  From here I configured ‘All Removable Storage Classes: Deny all access’ to Enable.

![Accounting GPO](https://i.ibb.co/7P4q9DP/Accounting-GPO-s-Enabled.png)


Sales staff often travel or work remotely, so enabling/configuring RDP access may be required for their role.  To do this, within the Group Policy Management Editor, I navigated to Computer Configuration, Policies, Administrative Templates, Windows Components, Remote Desktop Services, Remote Desktop Session Host then Connections.  I then configured ‘Allow users to connect remotely using Remote Desktop Services’ to Enable.  

![Sales GPO](https://i.ibb.co/Q34tb1T8/Sales-GPO-s-Enabled.png)

Once the Group Policy Objects have been implemented, it’s important to run the PowerShell command ‘gpupdate /force’ on the client machines so they are applied to the users.

