# Virtual-Server P1: Windows Server 2022 (Under Construction)
> Complete Virtual Network First!
## Overview
- Install Windows Server 2022
- Install VMware Tools
- Configure a Static IP
- Install Domain Service, DNS, and Certification Authority

## Windows Server 2022 Inital Setup
- [ ] VMware Config
- Network Adapter: Local LAN
- ISO [Windows Server 2022](https://info.microsoft.com/ww-landing-windows-server-2022.html) (Register for a free trial) 

### Installing VMware Tools (Recommended)
<img src="vmtool.gif"> <br>
- [ ] Install VMware tools
- Select `VM` > `Install VMware tools`
- Navigate to Windows File Explorer Select `DVD-VMware tools` > `Setup64`
- In the Setup Wizard Select `Complete` > `Next` > `Install` > `Finish` > `Reboot`

#### Check For Updates/SnapShot VM (Recommeneded)

### Rename This PC (Recommeneded)
- Select `Settings` > `System` > `About` > `Rename this PC` for example `WIN-DC`
#### Install your perfered Internet Browser (Optional)
- [ ] Chrome 
- [ ] Firefix
### Windows Preferences (Optional)
- Select `File Explorer` > `View` > `Options`
- [ ] Open File Explorer to `This PC`
- [ ] Privacy Uncheck both `Quick access`
- Select `View` in Folder Options
- [ ] Check `Display the full path in the title bar`
- [ ] Check `Show hidden files, folder, and drives`
- [ ] Uncheck `Hide extensions for known file types`
- Select `Apply`
#### Desktop Icons
- Select `Settings` > `Personalization` > ` Themes` > `Desktop icon settings`
- [ ] Select `Computer` `Network` `Recycle Bin` `Contronl Panel`
##### Snapshot VM (optional)
## Server Manager 
- [ ] Set a Static IP 
- Navigate to the `Server Manager` > `Local Server` > Select `IPv4 address assigned by DHCP,IPv6 enabled`
- Select `Ethernet0` > `Properties` > Uncheck `Internet Protocol Version 6`
- Select `Internet Protocol Version 4 (TCP/IPv4)`
- Select `Use the following IP address`
##### Add the Following 
- IP address `192.168.1.10`
- Default Gateway `192.168.1.1`
- Select `Use the following DNS Server addresses`
- Preferred DNS Server `192.168.1.10`
- Select `OK` > `OK` > Close > Exit
- Reboot
- [ ] Adding Server Roles
- Navigate to the `Server Manager` > `Manage` > `Add Roles and Features`
- Select `Next` > Select `Role-based` > `Next` > Select `a server from the server pool` > `Next`
- Select `Active Directory Domain Services`, and `DNS Server`
- Select `Add Features` > `Next` when prompted for each role
- Select `Next`
- [ ] Active Directory Domain Services
- Select `Next` 
- [ ] DNS Server
- Select `Next` > `Install` > Close 
- [ ] Active Directory Domain Configuration
- Navigate to the Flag Icon next to `Manage` 
- Select `Promote this server to a domain controller` > `Add a new forest`
- Add Root domain name: `CISO.net` (this can be anything you want) > `Next`
> Note! The Configuration wizard will be greyed out momentarily <br>  
- Add Password `Y0uR$uP3R$3Cr3tPas$w0Rd!` > `Next` > `Next` > `Next` > 'Next` > `Next` > `Next`
- Select `Install` 
##### Windows will reboot
> Note! This will take some time <br>
- [ ] Active Directory Certificate Service
> Note! Active Directory Domain Services need to be installed first for Enterprise CA <br>
- Navigate to the `Server Manager` > `Manage` > `Add Roles and Features`
- Select `Next` > Select `Role-based` > `Next` > Select `a server from the server pool` > `Next`
- Select `Active Directory Certificate Services` > `Next` > `Next` > `Next` > `Certification Authority`
- Select `Next` > `Install` > Close
- Navigate to the Flag Icon next to `Manage` 
- Select `Configure Active Directory Certificate Services...`
- Select `Next` > `Certification Authority` > `Enterprise CA` > `Root CA` > `Create a new private key`
- Select `Next` > `Next` > `Next` > `Next` > `Configure`
- Reboot
##### Snapshot VM (Recommended)
