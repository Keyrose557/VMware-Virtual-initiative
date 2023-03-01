# Virtual-Server P3: (Under Construction)
## Overview
- Create Domain Users
- Creating a CA Enrollment Agent
- Creating Certificate Templates
- Configure Digitial Certificate
- Enrolling Certificates on behalf of another
- Configure Smart Card Users
## Create Domain Users
- [ ] Server Manager 
- Select `Tools` > `Active Directory Users and Computers`
- Select `Users` > Right Click `Users` > `New` > `User`
- Properties > Account > Check `Smart Card is required for interactive logon` (for smart card users) <br>
Make four user accounts for testing
## Windows Certificate Authority
- [ ] [Check List](https://pivkey.zendesk.com/hc/en-us/articles/203127999-Requirements-for-Issuing-Smart-Card-Certificates) 
## Enrollment Agent
- [ ] Server Manager
- Select `Certification Authority` > `CISO-WIN-DC-CA` > Right Click `Certificate Template`> `Manage` > `Enrollment Agent`> Duplicate Template
- [ ] Properties of New Template
- Compatibility: <br>
Certification Authority `Windows Server 2016` <br>
Certificate recipient `Windows 10 / Windows server 2016` <br>
- General: <br>
Template display name `CISO Enrollment Agent` <br>
Check `Publish certificate in Active Directory`
- Request Handling <br>
Check `Prompt the user during enrollment and require user input when the private key is used`
-  Cryptography <br>
Check `Microsoft Base Smart Card Crypto Provider`
- Security <br>
Specify Group or user <br>
Required Permissions `enroll` <br>
> NOTE! You may want to create an AD group specifically for the Enrollment Agents for security. For educational purposes only I'll use Domain Admins <br>
Click `Ok` and Close Window
- [ ] Certificate Template
- Right CLick > `New` > `Certificate Template to Issue` > `CISO Enrollment Agent`

## Mapping PIV Certificate using OID
- [ ] Certification Authority CISO-WIN-DC-CA
- Right Click `Certificate Template`> `Manage` > `Smart Card Logon`> Duplicate Template
- Repeat Compatibility
- General <br>
Template display name `CISO Smartcard Logon`<br>
Check `Publish certificate in Active Directory`<br>
- Request Handling <br>
Purpose `Signature and Smartcard Logon` <br>
Check `Prompt the user during enrollment and require user input when the private key is used` <br>
- Cryptography <br>
Check `Request must use one of the following providers`<br>
Proiders `Microsoft Base Smart Card Crypto Provider`<br>
- Issuance Requirements <br>
Check `This number of authrized aignatures` `1`<br>
Application Policy `Certificate Request Agent`
- Security <br>
Specify Group or user <br>
Required Permissions `enroll` <br>
Click `Ok` and Close Window <br>
- [ ] Certificate Template
- Right CLick > `New` > `Certificate Template to Issue` > `CISO Smartcard logon`
<img src="cert1.png"> <br>
##  Issue your Enrollment Agent Certificate <br>
> Note! Use your Enrollment agent user <br>
- [ ] MMC.exe
- Select `File` > `Add Remove Snap-in` > `Certificates` > `My user account` > `Finish` > `Ok`
- Select `Certificates` > `Personal` > `Certificates` > Right Click `All Tasks` > `Request New Certifcate`
- Select `Next` > `Next` > Select `CISO Enrollment Agent` > `Ok` > `Finished`

## Enroll on Behalf of Others
> Note! Requires Enrollment Agent Certificate
- [ ] MMC.exe
- Select `Certificates` > `Personal` > `Certificates` > Right Click `All Tasks` > `Advanced Operations`> `Enroll on Behalf of`
- Select `Next` > `Next` > `Browse` > `OK` > `Next` > `CISO Smartcard Logon` > `Your Domain User` > `Enroll`
- Insert designated smart card & type pin 
- Wait a second 
<img src="piv1.gif">

## Testing our Configuration
<img src="pivt.gif"> <br>
- [ ] Check the PIV Keys Certificates <br>
### Challenge Join a Windows 10 VM to the Domain and login as a Domain User
<img src="pivt2.gif">

## Group Policy Management
- [ ] Think of the GPO as rules and policies for the Computers and Users in your domain
- More on this later...
