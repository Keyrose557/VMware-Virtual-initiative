# Enterprise Network Lab Template

<!-- Overview What is this... Required?
Also Table of Contents would be good here -->


[Back to labs](/labs/labs.md)

> **Disclaimer** !!!
The project is based off VMware Workstation on a windows machine. Issues/Configurations on Linux, MacOS, VMware Fusion, Hyper-V, and VirtualBox have not be tested.

## Getting Started

Your going to need to download the following **ISO's**

>Recommend You save these ISOs in a dedicated folder for organization

- [ ] VyOS <https://vyos.net/get/nightly-builds/>
- [ ] PFsense <https://www.pfsense.org/download/>
- [ ] Windows 11 <https://www.microsoft.com/software-download/windows11>
- [ ] Windows 10 <https://www.microsoft.com/en-us/software-download/windows10>
  - Use Windows Media Creation Tool to get the ISO
    - Create installation media (ISO file)
    - Use the recommended  options
    - ISO file
    - Specify File location

![Example](/media/video/win10.gif)

- [ ] Windows Server <https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2022>

- [ ] Red Hat Enterprise Linux
  - Create Free user account <https://www.redhat.com/wapps/ugc/register.html?_flowId=register-flow&_flowExecutionKey=e1s1>
  - You'll need to Activate a **Free** Individual Developer Subscription
  - Download RHEL iso

    ![Example](/media/video/RedhatISO.gif)

- [ ] Kali
  - Option 1: Installer Image (Requires configuration) <https://www.kali.org/get-kali/#kali-installer-images>
  - Option 2: Prebuild Virtual Machine (Ready to Boot) <https://www.kali.org/get-kali/#kali-virtual-machines>

### References

- VMware user guide <https://docs.vmware.com/en/VMware-Workstation-Pro/16.0/workstation-pro-16-user-guide.pdf>

- RHEL Workstation Install <https://developers.redhat.com/articles/2023/09/14/how-configure-rhel-workstation-during-installation#find_more_resources>

- RHEL Documentation  <https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/9?extIdCarryOver=true&intcmp=701f20000012k6JAAQ&sc_cid=7015Y000003sm2NQAQ>

- VyOS Documentation <https://docs.vyos.io/en/latest/>

- VyOs Quick Start <https://docs.vyos.io/en/latest/quick-start.html#quick-start>

## Environment Build Template

![NetworkMap](/media/images/Network%20Map.png)

### Virtual Network: WAN Router

**Overview :**

- [ ] Create a virtual router
- [ ] Install VyOS
- [ ] Configure network interfaces
- [ ] Configure DHCP/DNS
- [ ] Configure NAT
- [ ] Configure Firewall policies
- [ ] Verify Configuration
- [ ] Troubleshooting steps

### Create a Virtual Machine: VyOS WAN Router

![Example](/media/video/vm1vyos.gif)

- [ ] Create a New Virtual Machine
  - Select `Create a New Virtual Machine`
    - The New Virtual Machine Wizard will guide you through the process.
  - Select `Typical`
    - For the Guided approach
  - Select `Browse` and find the VyOS ISO
    - VMware needs to know where your OS is located.
    - It tries to detect its version but If unsure, reference supporting documents.
    - VyOS Documentation suggest `Debian 10`
  - Name your Virtual Machine, and Specify where it'll be saved.
    - I recommend having a dedicated space, defaults are fine
  - Select Disk Capacity.
    - If your unsure how much space you need start with recommeneded settings. You can always add more storage to a VM (User Preference)
    - Select `Store virtual disk as single file`

- [ ] VyOS Virtual Hardware Configuration
  - Select `Customize Hardware`
  - Select `Add`
  - Select `Network Adapter` > `Finish`
  - Select `Network Adapter 2` > `Lan Segments`
  - Select `Add` rename **LAN Segment 1** to **WAN**
    - Repeat and add LAN Segments named **LAN**, **DMZ**, and **OPT**
    - This creates the global LAN Segments that will be used in the lab
  - Select `OK`
  - Select **WAN** in the drop-down menu in **LAN Segment** for **Network Adapter 2**

- [ ] Option 1: Minimal specifications

  - Processor: 1 virtual CPU
  - Memory: 512 MB
  - Storage: 4GB
  - Network Adapter: NAT
  - Network Adapter 2: LAN Segment (WAN)

- [ ] Option 2: Recommended specifications

  - Processor: 1 virtual CPU
  - Memory: 1 GB
  - Storage: 10GB
  - Network Adapter: NAT
  - Network Adapter 2: LAN Segment (WAN)

- Select `Close` and `Finish` when hardware specs are chosen

#### References 2

- VyOS VMware Reference <https://vyos.io/solutions/vyos-on-vmware>

### Installing VyOS

![Example](/media/video/introvyos.gif)

- [ ] Boot up the VyOS VM and Install the ISO
  - Default Credentials :
    `User: vyos`
    `Password: vyos`
  - Run command

     ```bash
    install image
    ```

  - Accept defaults
  - Run command

    ```bash
    reboot
    ```

### VMware Snapshot (Recommended)

- [ ] Save a Snapshot of your VM
  - Select the snapshot icon to `Take a snapshot of this Virtual Machine`
   ![snapshot](/media/images/snapshot.png)
    - SnapShots enable you to revert your VM to this point in time.
    - Virtual SnapShots will help you save your progress in case of a mishap. Good notes will help you and your team troubleshoot.

![Example](/media/video/snap.gif)

### Quick Start VyOS

![VyOS_V1.4](/media/video/inter.gif)

- [ ] Configure VyOS router for Basic connectivity
  - Use config Command to enter Configuration mode

    ```bash
    configure
    ```

  - Interface configuration

    ```bash
    set interfaces ethernet eth0 address dhcp
    ```

    ```bash
    set interfaces ethernet etho0 description 'WAN'
    ```

    ```bash
    set interfaces ethernet eth1 address '172.31.1.1/24'
    ```

    ```bash
    set interfaces ethernet eth1 description 'LAN'
    ```

  - DHCP/DNS configuration

    ```bash
    set service dhcp-server shared-network-name LAN subnet 172.31.1.0/24 option default-router '172.31.1.1'
    ```

    ```bash
    set service dhcp-server shared-network-name LAN subnet 172.31.1.0/24 option name-server '172.31.1.1'
    ```

    ```bash
    set service dhcp-server shared-network-name LAN subnet 172.31.1.0/24 option domain-name 'vyos.net'
    ```

    ```bash
    set service dhcp-server shared-network-name LAN subnet 172.31.1.0/24 lease '86400'
    ```

    ```bash
    set service dhcp-server shared-network-name LAN subnet 172.31.1.0/24 range 0 start '172.31.1.9'
    ```

    ```bash
    set service dhcp-server shared-network-name LAN subnet 172.31.1.0/24 range 0 stop '172.31.1.50'
    ```

    ```bash
    set service dhcp-server shared-network-name LAN subnet 172.31.1.0/24 subnet-id '1'
    ```

    ```bash
    set service dns forwarding cache-size '0'
    ```

    ```bash
    set service dns forwarding listen-address '172.31.1.1'
    ```

    ```bash
    set service dns forwarding allow-from '172.31.1.0.0/24'
    ```

  - Network Address Translation Configuration

    ```bash
    set nat source rule 100 outbound-interface name 'eth0'
    ```

    ```bash
    set nat source rule 100 source address '172.31.1.0/24'
    ```

    ```bash
    set nat source rule 100 translation address masquerade
    ```

  - Firewall configuration

    ```bash
    set firewall group interface-group WAN interface eth0
    ```

    ```bash
    set firewall group interface-group LAN interface eth1
    ```

    ```bash
    set firewall group network-group NET-INSIDE-v4 network '172.31.1.0/24'
    ```

  - Global State Policies

    ```bash
    set firewall global-options state-policy established action accept
    ```

    ```bash
    set firewall global-options state-policy related action accept
    ```

    ```bash
    set firewall global-options state-policy invalid action drop
    ```

  - Block Incoming Traffic

    ```bash
    set firewall ipv4 name OUTSIDE-IN default-action 'drop'
    ```

    ```bash
    set firewall ipv4 forward filter rule 100 action jump
    ```

    ```bash
    set firewall ipv4 forward filter rule 100 jump-target OUTSIDE-IN
    ```

    ```bash
    set firewall ipv4 forward filter rule 100 inbound-interface group WAN
    ```

    ```bash
    set firewall ipv4 forward filter rule 100 destination group network-group NET-INSIDE-v4
    ```

    ```bash
    set firewall ipv4 input filter default-action 'drop'
    ```

  - Allow Services

    ```bash
    set firewall ipv4 input filter rule 30 action 'accept'
    ```

    ```bash
    set firewall ipv4 input filter rule 30 icmp type-name 'echo-request'
    ```

    ```bash
    set firewall ipv4 input filter rule 30 protocol 'icmp'
    ```

    ```bash
    set firewall ipv4 input filter rule 30 state new
    ```

    ```bash
    set firewall ipv4 input filter rule 40 action 'accept'
    ```

    ```bash
    set firewall ipv4 input filter rule 40 destination port '53'
    ```

    ```bash
    set firewall ipv4 input filter rule 40 protocol 'tcp_udp'
    ```

    ```bash
    set firewall ipv4 input filter rule 40 source group network-group NET-INSIDE
    ```

    ```bash
    set firewall ipv4 input filter rule 50 action 'accept'
    ```

    ```bash
    set firewall ipv4 input filter rule 50 source address 127.0.0.0/8
    ```

    ```bash
    commit
    ```

    ```bash
    save
    ```

### Verify the configuration

![Example](/media/video/router1.gif)

- [ ] Test that the configuration works
  - Ping 8.8.8.8 from the Vyos Router
  - Ping the VyOS from another VM
  - Verify that a VyOS Router DHCP service is working
  - Verify Hosts connected to the VyOS Router have internet connectivity

#### Quick Testing method

- Use a Prebuilt Virtual Machine (Kali Linux) <https://www.kali.org/get-kali/#kali-virtual-machines>
  - Use the recommended download
  - Extract the Kali zip file in your Virtual WorkSpace File
  - Try **7zip**, for extracting zip files
    <https://www.7-zip.org/download.html>
  - Change the network adapter to `LAN segment: WAN`
  - ping your router with command `ping 172.31.1.1`
  - Its a good idea to test connectivity with a simple google search

#### Basic Connectivity 🫠

![Example](/media/video/kalipre.gif)

### Troubleshooting steps

- [ ] Restart the VM
- [ ] Verify VyOS configuration

   ```bash
   show configuration
   ```

  - Typos are very common, check for errors
  - VyOS Documentation is very helpful incase you get stuck in the Command Line trying to correct a typo.

- [ ] Verify network adapter on VMware
  - Check the VMs are assigned the proper **Network Adapters**
- [ ] Reference Documentation and Resources

### References 3

- VyOS User Guide Quick Start <https://docs.vyos.io/en/latest/quick-start.html>
- Vyos Command Line Interface <https://docs.vyos.io/en/latest/cli.html>
- VyOS Cheat Sheet <https://github.com/bertvv/cheat-sheets/blob/master/docs/VyOS.md>

### Virtual Network: Firewall

Overview

- [ ] Create a Virtual Firewall
- [ ] Install pfSense
- [ ] Configure network interfaces
- [ ] Configure DHCP
- [ ] Configure NAT
- [ ] Configure Firewall policies

#### Required Downloads & Documentation

- pfSense <https://www.pfsense.org/download>
  - Architecture `AMD64 (64-bit)`
  - Installer `DVD Image (ISO) Installer`
  - Mirror `Austin, TX USA`
- pfSense Documentation <https://docs.netgate.com/pfsense/en/latest/?_gl=1*2oi9it*_ga*MTkyNjgxODg3NC4xNjc2MjM4NDUz*_ga_TM99KBGXCB*MTY3NjIzODQ1Mi4xLjEuMTY3NjIzODg3OS4wLjAuMA..>
- pfSense VMware Reference <https://docs.netgate.com/pfsense/en/latest/recipes/virtualize-esxi.html>
- pfSense Install guide <https://docs.netgate.com/pfsense/en/latest/install/install-walkthrough.html>

### Create a Virtual Firewall: PfSense

![example](/media/video/pfvm.gif)

- New Virtual Machine Wizard: will guide you through the process just like last time.
- FreeBSD based

#### pfSense Virtual Hardware reference

- Netgate 4200 <https://www.netgate.com/pfsense-plus-software/how-to-buy#appliances>
- We'll be referencing Netgate appliances for hardware specifications.

#### Virtual specifications

- Processor: 1 virtual CPU, 2 virtual Cores
- Memory: 4 GB
- Storage: 128GB
- Network Adapter: LAN Segment (WAN)
- Network Adapter 2: LAN Segment (LAN)
- Network Adapter 3: LAN Segment (DMZ)

#### Low on Physical Resources

- Reference Netgate 1100 or 2200 appliance technical specs
- Reduce number of cores per processor
- Use recommend memory indicated by Virtual Machine Settings
- Reduce Hard Disk Size

### Installing pfSense

![Example](/media/video/pfvm10.gif)

- Installation Walkthrough <https://docs.netgate.com/pfsense/en/latest/install/install-walkthrough.html>
  - Default install
- pfSense Configuration Documentation <https://docs.netgate.com/pfsense/en/latest/config/index.html>

### pfSense webConfigurater

![Example](/media/video/pfweb.gif)

- We'll be using the pre built VM to access on pfSense webGUI. The two VMs need to be in the same network.

#### Accessing pfSense webConfigurator

![Example](/media/images/pfw.png)

- pfSense by default is accessed on `192.168.1.1`
- A seperate VM needs to be on this network to access web GUI

#### Initial Configuration

- [ ] pfSense Setup Wizard <https://docs.netgate.com/pfsense/en/latest/config/setup-wizard.html>

  - Default Credentials
`User: admin`
`Password: pfsense`

- [ ] Update LAN IP Address
  - LAN IP Address `192.168.3.1`
  - Admin Password `SecretPassword`

- [ ] Verify Basic Connectivity
  - Ping your devices
  - Access the web
  - Taking a Snapshot of the pfSense VM is recommended

![Example](/media/images/pfv.PNG)

#### Additional Configurations (Web GUI)

- [ ] Enable Virtual Adapters
  - Navigate to `Interfaces` > `Assignment`
  - Select `+ Add` for `em2` and `em3`
  - Save

> Note! Check out what VMware is doing with the network adapter using LAN Segment WAN = em0 LAN = em1 DMZ = em2 OPT = em3

- [ ] Rename Interfaces
  - Navigate to `Interfaces` > `OPT2`
  - Select `Enable Interface`
  - Description `DMZ`
  - IPv4 Configuration Type `Static IPv4`
  - IPv4 Address `10.0.1.1` / `24`
  - Save
  - Apply Changes

- [ ] Enable DHCP
  - Navigate to `Services` > `DHCP Server`
  - Select `DMZ` and `Enable`
  - Add `Address Pool Range` > `From` 10.0.1.10 > `To` 10.0.1.50
  - Save & Apply changes

- [ ] Initial Firewall Rule
  - Navigate to `Firewall` > `Rules` > `LAN`
  - Navigate to `Actions` Select Box icon `Copy` on second rule
  - Change Interface `DMZ` Source `DMZ subnet`
  - Save & Apply

- [ ] Traffic Routing
  - Navigate to `System` > `Routing` > `Gateways`
  - Add Interface `LAN` Name `LAN_GW` Gateway `192.168.3.10` (ip address of LAN router eth0)
  - Save & Apply
  - Navigate to `Static Routes`
  - Add Destination Network `192.168.1.0` / `24` Gateway `LAN_GW-192.168.3.10`

#### Troubleshooting steps 2

- [ ] Restart VM
- [ ] Increase VM RAM
- [ ] Verify network adapter on VMware
- [ ] Verify Configuration settings
- [ ] Reference Documentation and Resources

#### References 4

- pfSense Documentation <https://docs.netgate.com/pfsense/en/latest/preface/index.html>

### Virtual LAN Router Challenge

- Try and configure another router on your own
  - [ ] Create & Configure a LAN router
  - [ ] Create and Configure two VMs
    - One in the DMZ
    - One in the LAN
    - Reference the Network map
  - [ ] Successfully ping from the 10.0.1.0/24 network (DMZ) to the 192.168.1.0/24 (LAN)

#### Troubleshooting steps 3

- [ ] Check your Network Adapters
- [ ] Check your Networking Configuration
- [ ] Increase VM resources

#### Hints for the LAN router

- [ ] Virtual Machine Hardware
  - Network Adapter: LAN Segment (LAN)
  - Network Adapter 2: LAN Segment (OPT)
- [ ] VyOS Configuration Hint
  - eth0 = 192.168.3.10
  - eth1 = 192.168.1.1
- [ ] Using multiple VMs can be helpful when test connectivity

![Example](/media/images/lan.PNG)

### Good Luck on the challenge

Collaborate with your colleagues and ask for help if you get stuck.

- Use the reference material and remember the internet is full of helpful info

The gif below should give you an idea of successfully verifying connectivity of the network.

![Example](/media/video/hint.gif)

- We'll Go over any questions/issues during our alloted time

#### References 5

- VyOS User Guide <https://docs.vyos.io/en/latest/index.html>
- Quick Start <https://docs.vyos.io/en/latest/quick-start.html>

#### Troubleshooting steps 4

- [ ] Restart VM
- [ ] Verify VyOS configuration `show config`
- [ ] Verify VyOs interfaces `show interfaces`
- [ ] Verify network adapter on VMware
- [ ] Reference Documentation and Resources

<details>
<summary><b> Challenge Help</b></summary>

- Below is enough to ensure you have connectivity if your following the IP scheme. Just remember it still needs a more robust configuration. The following config is to help new students catch up

- [ ] VyOS router for Basic connectivity
  - Use config Command to enter Configuration mode

    ```bash
    configure
    ```

  - Interface configuration

    ```bash
    set interfaces ethernet eth0 address dhcp
    ```

    ```bash
    set interfaces ethernet eth1 address '192.168.1.1/24'
    ```

    ```bash
    set interfaces ethernet eth0 description WAN

    Set interfaces ethernet eth1 description LAN
    ```

  - DHCP/DNS configuration

    ```bash
    set service dhcp-server shared-network-name LAN subnet 192.168.1.0/24 option default-router '192.168.1.1'
    ```

    ```bash
    set service dhcp-server shared-network-name LAN subnet 192.168.1.0/24 option name-server '192.168.1.1'
    ```

    ```bash
    set service dhcp-server shared-network-name LAN subnet 192.168.1.0/24 lease '86400'
    ```

    ```bash
    set service dhcp-server shared-network-name LAN subnet 192.168.1.0/24 range 0 start '192.168.1.9'
    ```

    ```bash
    set service dhcp-server shared-network-name LAN subnet 192.168.1.0/24 range 0 stop '192.168.1.50'
    ```

    ```bash
    set service dhcp-server shared-network-name LAN subnet 192.168.1.0/24 subnet-id '1'
    ```

    ```bash
    set service dns forwarding cache-size '0'
    ```

    ```bash
    set service dns forwarding listen-address '192.168.1.1'
    ```

    ```bash
    set service dns forwarding allow-from '192.168.1.0/24'
    ```

  - Network Address Translation Configuration

    ```bash
    set nat source rule 100 outbound-interface name 'eth0'
    ```

    ```bash
    set nat source rule 100 source address '192.168.1.0/24'
    ```

    ```bash
    set nat source rule 100 translation address masquerade
    ```

  - Firewall configuration

    ```bash
    set firewall group interface-group WAN interface eth0
    ```

    ```bash
    set firewall group interface-group LAN interface eth1
    ```

    ```bash
    set firewall group network-group NET-INSIDE-v4 network '172.31.1.0/24'
    ```

  - Global State Policies

    ```bash
    set firewall global-options state-policy established action accept
    ```

    ```bash
    set firewall global-options state-policy related action accept
    ```

    ```bash
    set firewall global-options state-policy invalid action drop
    ```

</details>

### Network Template Summary

- [ ] VyOS Edge Router
  - Login User `vyos`
  - Password `vyos`
  - subnet `172.31.1.0/24`
- [ ] pfSense Firewall
  - Login user `admin`
  - Password `pfsense`
  - subnet `192.168.3.0/24`
- [ ] DMZ
  - subnet `10.0.1.0/24`
- [ ] VyOS LAN router
  - Login User `vyos`
  - Password `vyos`
  - subnet `192.168.1.0/24`

If your following along, the following setting and configurations are just enough to get connectivity amongst all the machines in the environment. It is on the students to configure and secure the rest as we slowly start introducing new machines and new services.

The objective is to encourage students to collaborate and assist each other on applying learned skills while also developing new ones.

Occasionally, We'll include a challenge to facilitate a discussion and collaboration amongst students of all levels.

#### Cyber Challenges

- VyOS Edge Router
  - [ ] Harden the VyOS router
  - [ ] Demonstrate an alternative configuration

- pfSense Firewall VM
  - [ ] Harden the Firewall
  - [ ] Create effective Firewall rules
  - [ ] Demonstrate alternative configuration
  - [ ] Secure the DMZ from the LAN
  - [ ] Enable network traffic analysis capabilities

- LAN Router
  - [ ] Harden the router
  - [ ] Demonstrate an functioning configuration

### Windows Server 2022

> Complete Virtual Network First

#### Overview

- [ ] Install Windows Server 2022
- [ ] Install VMware Tools
- [ ] Configure a Static IP
- [ ] Install Domain Service, DNS, and Certification Authority

### Windows Server 2022 Initial Setup

- VMware Config
  - Network Adapter: Local LAN
  - ISO Windows Server 2022 <https://info.microsoft.com/ww-landing-windows-server-2022.html> (Register for a free trial)
  - Hardware requirements <https://learn.microsoft.com/en-us/windows-server/get-started/hardware-requirements?tabs=cpu>

- [ ] Install VMware tools
- Select `VM` > `Install VMware tools`
- Navigate to Windows File Explorer Select `DVD-VMware tools` > `Setup64`
- In the Setup Wizard Select `Complete` > `Next` > `Install` > `Finish` > `Reboot`

![example](/media/video/vmtool.gif)

#### Check For Updates/SnapShot VM (Recommended)

- [ ] Rename This PC (Recommended)
  - Select `Settings` > `System` > `About` > `Rename this PC` for example `WIN-DC`

#### Install your preferred Internet Browser (Optional)

- [ ] Chrome
- [ ] Firefox
- [ ] Brave
- [ ] Other

#### Windows Preferences (Optional)

- Select `File Explorer` > `View` > `Options`
- Open File Explorer to `This PC`
- Privacy Uncheck both `Quick access`
- Select `View` in Folder Options
- Check `Display the full path in the title bar`
- Check `Show hidden files, folder, and drives`
- Uncheck `Hide extensions for known file types`
- Select `Apply`

#### Desktop Icons

- Select `Settings` > `Personalization` > `Themes` > `Desktop icon settings`
- Select `Computer` `Network` `Recycle Bin` `Control Panel`

#### Snapshot VM (reminder)

### Server Manager

- [ ] Set a Static IP
  - Navigate to the `Server Manager` > `Local Server` > Select `IPv4 address assigned by DHCP,IPv6 enabled`
  - Select `Ethernet0` > `Properties` > Uncheck `Internet Protocol Version 6`
  - Select `Internet Protocol Version 4 (TCP/IPv4)`
  - Select `Use the following IP address`
- [ ] Add the Following
  - IP address `192.168.1.10`
  - Default Gateway `192.168.1.1`
  - Select `Use the following DNS Server addresses`
  - Preferred DNS Server `192.168.1.10`
  - Select `OK` > `OK` > Close > Exit
  - Reboot

- [ ] Add Server Roles
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

> Note! The Configuration wizard will be greyed out momentarily

- Add Password `Y0uR$uP3R$3Cr3tPas$w0Rd!` > `Next` > `Next` > `Next` > `Next` > `Next` > `Next`
- Select `Install`
- **Windows will reboot**

> Note! This will take some time

- [ ] Active Directory Certificate Service

> Note! Active Directory Domain Services need to be installed first for Enterprise CA

- Navigate to the `Server Manager` > `Manage` > `Add Roles and Features`
- Select `Next` > Select `Role-based` > `Next` > Select `a server from the server pool` > `Next`
- Select `Active Directory Certificate Services` > `Next` > `Next` > `Next` > `Certification Authority`
- Select `Next` > `Install` > Close
- Navigate to the Flag Icon next to `Manage`
- Select `Configure Active Directory Certificate Services...`
- Select `Next` > `Certification Authority` > `Enterprise CA` > `Root CA` > `Create a new private key`
- Select `Next` > `Next` > `Next` > `Next` > `Configure`
- Reboot

#### Snapshot VM (Reminder)

### Virtual-Hosts

>Note! Easy Install in VMware will use auto-login (Not recommended)

- Overview
  - [ ] Domain Join a Windows & Linux VM

#### Windows Domain Prep & Join

- [ ] Create a Windows 10 VM
  - LAN Segment `LOCAL LAN`
  - Enable Device Passthrough in VM `.vmx` File
    - `usb.generic.allowHID = "TRUE"`
    - `usb.generic.allowLastHID = "TRUE"`
  - Make your Domain Controller your VM's DNS server
- [ ] Join Domain for Windows
  ![example](/media/video/dom1.gif)
- Select `Settings` > `Accounts` > `Access work or school` > `Connect` > `Join this device to local Active Domain`
- Domain Name `CISO.net` (If not found, verify your DNS configurations)

- Domain Credentials Use an Administrative account to authorize the domain join

### Rhel Installation

- [ ] Create a Rhel VM
  - LAN Segment `LOCAL LAN`
  - Enable Device Passthrough in VM `.vmx` File
    - `usb.generic.allowHID = "TRUE"`
    - `usb.generic.allowLastHID = "TRUE"`
- [ ] Create a Red Hat Account
  - <https://sso.redhat.com/auth/realms/redhat-external/login-actions/registration?client_id=https%3A%2F%2Fwww.redhat.com%2Fwapps%2Fugc-oidc&tab_id=x5ikI1GYHSs> (Required)
- [ ] ISO Download <https://developers.redhat.com/products/rhel/download>
- [ ] Connect to Red Hat
  ![example](/media/images/Rhel.PNG)

- Software Selection (I encourage you to explore the options)
  - Basic Environment `Workstation`
  - Additional Software `Smart Card Support`
- Network & Host Name
  - Hostname `RHEL9W` (OptionalName the host anything you'd like)
  - Make your Domain Controller your VM's DNS server
- Root Password `Y0uR$up3r$3cr3tP@ssW0rd!`
For instructional Purposes Only I used a short insecure password
- Begin Installation

- [ ] Red Hat Registration Check
  ![example](/media/images/rhel2.png)
  - Verify your RHEL VM can update packages
  - run the command

    ```bash
    yum update
    ```

  - Reboot if Machine fails to update
  - Verify Red Hat Subscription

#### Rhel Domain Prep

> Note! By default Network Manager on RHEL dynamically update the resolv.conf, You can disable this.

- [ ] Our Rhel Workstation Needs to use our AD as a DNS Server
![example](/media/images/rhel3.PNG)

  - Method 1

    ```bash
    nano /etc/resolv.conf
    ```

    - Add `nameserver 192.168.1.10`
    Go to Settings and Disable Automatic DNS
- Method 2

  - Select `Settings` > `Network` > Select the Gear Icon in `Wired`> `IPv4`
  - Disable `Automatic` > In DNS specify your AD IP address
- Method 3
Rhel Documentation <https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/configuring_and_managing_networking/manually-configuring-the-etc-resolv-conf-file_configuring-and-managing-networking#doc-wrapper>

- [ ] Verify Rhel can find your Domain
  - Command `realm discover` `Name Of your Domain`
  Use Command `realm --help` for more info

    ```bash
    realm discover CISO.net
    ```

    ![example](/media/images/rhel5.PNG)

- [ ] Install required Packages
  - Command `yum install packages sssd realmd oddjob oddjob-mkhomedir adcli samba-common samba-common-tools krb5-workstation openldap-clients policycoreutils-python-utils`

    ```bash
    yum install packages sssd realmd oddjob oddjob-mkhomedir adcli samba-common samba-common-tools krb5-workstation openldap-clients policycoreutils-python-utils
    ```

![Example](/media/images/rhel4.PNG)

#### Rhel Domain Join

![example](/media/video/rheld.gif)

- [ ] Verify Rhel can pull Domain User Credentials
  - Command `id [username]@[domain_name]`

    ```bash
    id Q1@CISO.net
    ```

![example](/media/images/rhel6.PNG)

- [ ] Verify Domain Users can Logon
![example](/media/video/rheld1.gif)
- user `domain_username@your_domain_name.net`
- password `your_domain_user_password`

- [ ] Enable Dynamic DNS
  - Command
  ```bash
  sudo nano /etc/sssd/sssd.conf
  ```
  - Add the following:
`default_domain_suffix = YourDomainName`
`ad_hostname = yourHostname.domain_name`
`dyndns_update = True`
`dyndns_refresh_interval = 43200`
`dyndns_update_prt = True`
`dyndns_ttl = 3600`
`dyndns_auth = GSS-TSIG`
![example](/media/images/rhel7.PNG)
  - Use command

  ```bash
  systemctl restart sssd
  ```

![example](/media/video/rheld2.gif)

#### Whats the difference

- You dont have to type `username@domain.com` we now just type our `domain_username` 😌
- Check your Windows Sever DNS Manager, your Dynamic DNS updates are working. No manual DNS record labor needed 💅🏾

![example](/media/images/rhel8.PNG)

#### References 6

- Rhel Integration with Windows Active Directory <https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/integrating_rhel_systems_directly_with_windows_active_directory/index>
- Rhel Domain Join article <https://www.redhat.com/sysadmin/linux-active-directory>

### Challenge Create A Server VM & Join the Domain

![example](/media/video/adhint2.gif)

- Heres a hint: DNS is your best friend
- [ ] Deploy a Rhel Server and Windows server in the DMZ network
- [ ] Join the Domain
- [ ] Verify Domain User Authentication

### Windows server Domain join is slightly different

![EXAMPLE](/media/video/adhint.gif)

#### Discussion

- Why join a Domain ?
- What is DNS ?
- What is an Active Directory
- What is a Domain Controller

### Expanding Device Passthrough (optional)

**Overview**

- [ ] Configure Device Passthrough
- [ ] Installing Smart Card Drivers
- [ ] Testing Initial Config & Hardwae

#### Additional Hardware support

- Smart Card Reader <https://www.amazon.com/Identiv-SCR3310v2-0-Smart-Card-Reader/dp/B002N3MM6W/ref=sr_1_3?keywords=smart+card+reader&qid=1677462287&sprefix=smart+car%2Caps%2C182&sr=8-3>
- PIV Smart Card<https://www.amazon.com/Taglio-Certificate-Authentication-Identification-Contactless/dp/B00SJV2CNK/ref=d_pb_allspark_dp_sims_pao_desktop_session_based_vft_med_sccl_3_2/130-9823239-2457105?pd_rd_w=lDNmz&content-id=amzn1.sym.6b5008ac-c24a-4aea-a3ea-015a531184f5&pf_rd_p=6b5008ac-c24a-4aea-a3ea-015a531184f5&pf_rd_r=ZN1Y9G74ES0PV9AQ6X11&pd_rd_wg=LXSF5&pd_rd_r=508a86fd-92f9-4e2c-9c3e-e156ae9c9c52&pd_rd_i=B00SJV2CNK&psc=1>
- Yubikey 5 NFC <https://www.yubico.com/product/yubikey-5-nfc/>

#### Updating the Virtual Machine's Configuration

![example](/media/images/pass.png)

- [ ] Device Passthrough with VMware Workstation
  1. Shut down the virtual machine
  2. Locate the VM's .vmx configuration file
  3. Open the configuration file with a text editor
  4. Add the two lines below to the file and save it

  `usb.generic.allowHID = "TRUE"`
  `usb.generic.allowLastHID = "TRUE"`

![example](/media/images/vmx.PNG)

#### VMware Device Passthrough

![example](/media/video/smartc.gif) 

- In VMware's bottom right corner you can select a device to passthrough/connect to your vm

#### Windows Server SmartCard Reader Driver Fix

![Example](/media/video/drive.gif)

- [ ] `UMDF2` Microsoft Usbccid Smartcard Reader needs to replaced by `WUDF`
  - Windows Server has a driver issue `UMDF2`
  - Navigare to the `Device Manager` > `Smart Card Readers` > `Properties` > `Driver` > `Update Driver` > `Browse my computer for drivers` > `Let me pick from a list of available drivers on my computer`
  - Select  `WUDF` > Next > Close

#### Test Your Configuration

![example](/media/video/ctest.gif)

- [ ] PIVKey Test <https://pivkey.com/starttest/>
  - Using your VM test that your smart card and reader is working properly
  - Note that you will have to physically insert your smart card

![example](/media/video/yutest.gif)

- [ ] YubiKey Test <https://demo.yubico.com/webauthn-technical/registration>
  - Note that you will have to physically touch your yubikey it will light up green
  - Yubikey Guides <https://support.yubico.com/hc/en-us/articles/360013707820-YubiKey-Smart-Card-Deployment-Guide>

#### Additional Downloads for PIV SmartCard

- [ ] PIVKey Admin Installer <https://pivkey.zendesk.com/hc/en-us/articles/203863995-PIVKey-Admin-Installer>
  - I highly recommend `README.txt`
  - Smart Card Documentation<https://pivkey.zendesk.com/hc/en-us>
  - Select `PIVkey Installer-Admin-7.1.0.17.exe` (required)
  - Select `vSEC_CMS_K2.0.exe` (optional)

[labs](/labs/labs.md)
