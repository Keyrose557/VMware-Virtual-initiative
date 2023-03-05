# Virtual-Host P1: (Under Construction)<br>
>Note! Easy Install in VMware will use autologin (Not recommended)
## Overview
- Domain Joins
- Windows & Linux
## Windows Domain Prep & Join
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
- [ ] Create a Rhel VM
- LAN Segment `LOCAL LAN`
- Enable Device Passthrough in VM `.vmx` File <br>
`usb.generic.allowHID = "TRUE"` <br>
`usb.generic.allowLastHID = "TRUE"` <br>
- [ ] [Create a Red Hat Account](https://sso.redhat.com/auth/realms/redhat-external/login-actions/registration?client_id=https%3A%2F%2Fwww.redhat.com%2Fwapps%2Fugc-oidc&tab_id=x5ikI1GYHSs) (Required)
- [ ] [ISO Download](https://developers.redhat.com/products/rhel/download)
- [ ] Create a VM
- Connect to Red Hat <br>
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
Make your Domain Controller your VM's DNS server <br>
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
## Rhel Domain Prep <br>
> Note! By default Network Manager on RHEL dynamically update the resolv.conf, You can disable this <br>
- [ ] Our Rhel Workstation Needs to use our AD as a DNS Server <br>
<img src="rhel3.PNG"> <br>
- Method 1 <br>
`nano /etc/resolv.conf` <br>
Add `nameserver 192.168.1.10` <br>
Go to Settings and Disable Automatc DNS <br>
- Method 2 <br>
Select `Settings` > `Network` > Select the Gear Icon in `Wired`> `IPv4` <br>
Disable `Automatic` > In DNS specify your AD IP address <br>
- Method 3 <br>
[Rhel Documentation](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/configuring_and_managing_networking/manually-configuring-the-etc-resolv-conf-file_configuring-and-managing-networking#doc-wrapper)
- Verify Rhel can find your Domain <br>
Command `realm discover` `Name Of your Domain` <br>
Use Command `realm --help` for more info <br>
<img src="rhel5.PNG"> <br>
- [ ] Install required Packages <br>
- Command `yum install sssd realmd oddjob oddjob-mkhomedir adcli samba-common samba-common-tools krb5-workstation openldap-clients policycoreutils-python-utils`
<img src="rhel4.PNG"> <br>
## Rhel Domain Join <br>
<img src="rheld.gif"> <br>
- [ ] Verify Rhel can pull Domain User Credentials
- Command `id [username]@[domainame]` <br>
<img src="rhel6.PNG"> <br>
- [ ] Verify Domain Users can Logon <br>
<img src="rheld1.gif"> <br>
- user `domain_username@your_domain_name.net`
- password `your_domain_user_password`
## Preferences (Highly Recommended)
- [ ] Easier Logins & Dynamic DNS
- Command `sudo nano /etc/sssd/sssd.conf`
- Add the following: <br>
`default_domain_suffix = YourDomainName` <br>
`ad_hostname = yourHostname.domainname` <br>
`dyndns_update = True` <br>
`dyndns_refresh_interval = 43200` <br>
`dyndns_update_prt = True` <br>
`dyndns_ttl = 3600` <br>
`dyndns_auth = GSS-TSIG` <br>
- You will need to use command `systemctl restart sssd` to ensure changes are applied
<img src="rhel7.PNG"> <br>
<img src="rheld2.gif"> <br>
### Whats the diffrence
- You make dont have to type `username@domain.com`, instead type just the `domain_username` 😌
- Check your Windows Sever DNS Manager, your Dynamic DNS updates are working. No maunal DNS record labor needed 💅🏾
<img src="rhel8.PNG">

## References
- [ ] [Rhel Integration with Windows Active Directory ](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/integrating_rhel_systems_directly_with_windows_active_directory/index)
- [ ] [Rhel Domain Join article](https://www.redhat.com/sysadmin/linux-active-directory)

## Challenge Create A Server VM & Join the Domain <br>
<img src="adhint2.gif"> <br>
- Heres a hint: DNS is your best friend or worst enemey 
- [ ] Deploy a Rhel Server and Windows server in the DMZ network
- [ ] Join the Domain 
- [ ] Verify Domain User Authentication <br>
<img src="adhint.gif"> <br>
- Windows server Domain join is slightly different
## Discussion 
- Why join a Domain ?
