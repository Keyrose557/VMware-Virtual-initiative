# Virtual-Host P1: (Under Construction)<br>
>Note! Easy Install in VMware will use autologin (Not recommended)
## Overview
- Domain Joins
- Windows & Linux
## Windows Domain Join
- [ ] Create a Windows 10 VM
- LAN Segment `LOCAL LAN`
- Enable Device Passthrough in VM `.vmx` File <br>
`usb.generic.allowHID = "TRUE"` <br>
`usb.generic.allowLastHID = "TRUE"` <br>
- Make your Domain Controller your VM's DNS server
- [ ] Join Domain for Windows <br>
<img src="dom1.gif"> <br>
- Select `Settings` > `Accounts` > `Access work or school` > `Connect` > `Join this device to local Active Domain`
- Domain Name `CISO.net` <br>
If not found, verify your DNS configurations
- Domain Credentials <br>
Use an Administrative account to authorize the domain join <br>
## Rhel Installation 
- [ ] [Create a Red Hat Account](https://sso.redhat.com/auth/realms/redhat-external/login-actions/registration?client_id=https%3A%2F%2Fwww.redhat.com%2Fwapps%2Fugc-oidc&tab_id=x5ikI1GYHSs) (Required)
- [ ] [ISO Download](https://developers.redhat.com/products/rhel/download)
- [ ] Create a VM
- Connect to Red Hat
<img src="Rhel.PNG"> <br>
- Software Selection <br>
> Note! I encourage you to play with the additional options <br>
- Basic Environment <br>
`Workstation`
- Additional Software <br> 
`Smart Card Support` <br>
- Network & Host Name <br>
Hostname `RHEL9W` (Optional) <br>
Name the host anything you'd like <br>
- Root Password <br>
`Y0uR$up3r$3cr3tP@ssW0rd!`<br>
For instructional Purposes Only I used a short insecure password
- Begin Installation
- [ ] Red Hat Registration Check <br>
<img src="rhel2.png"> <br>
- [ ] Verify your RHEL VM can update packages
- run the command `yum update`
- Reboot if Machine failes to update
- Verify Red Hat Subscription 
