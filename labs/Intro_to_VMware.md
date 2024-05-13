# Intro to VMware

A quick tutorial on VMware

[Home](/README.md)
[Labs](/labs/labs.md)

## Get familiar with VMware Workstation

- [ ] Set a Default Location for your Virtual Machines.

    1. Select `Edit` > `Preference`
    2. Select `Browse...`
       1. You can keep the Default but for organizational purposes I recommend a designated storage space.
       2. Optionally, I recommend creating folders for managing different virtual environments.

![Example](/media/video/labspace.gif)

## Virtual Network Editor

- [ ] Configure the Virtual Network adapters.

    1. Select `Edit` > `Virtual Network Editor`
    This will open a new window. By default VMware creates 3 types of Network adapters named `VMnet0`, `VMnet1` and `VMnet8`.

    2. Select `Change Settings` (if your customizing your network settings)

>VMware by default handles the DHCP, Subnet IP , Netmask, IP ranges, and IP leases for your virtual environment.

![Example2](/media/video/VNE.gif)

### Here is a simplified summary of VMware's virtual network adapters

#### Bridge

- This will expose your VM to the Network your host machine is on. So be careful/aware.
- This project will **NOT** be using the Bridge network adapter

#### NAT

- The VM will have its own private network, with DHCP. However, the VM will share your host IP address for internet access.

#### FUN FACT: NAT stands for Network Address Translation

#### Host-only

- This creates a private/isolated network within the host, with DHCP. Think of it as a private sandbox for your experiments.

#### LAN Segments

- The virtual machine uses a private network that can be shared with other virtual machines.
- This network adapter does not provide a DHCP server for you.
- You must manually configure IP addressing for virtual machines on a LAN segment.
- You can either configure a DHCP server on the LAN segment to allocate IP addresses, or you can configure a fixed IP address for each virtual machine on the LAN segment.

#### Subnet IP

- The Virtual Network Editor allows your to specify your Network address and Subnet Mask.

#### DHCP Settings

- **Dynamic Host Configuration Protocol**
  - Assigns your IP addresses for your Virtual Machines.
  - Don't forget about the IP leases. This is how long a host's ip address are assigned.

#### Reference the Vmware's User Guide for more details

- <https://docs.vmware.com/en/VMware-Workstation-Pro/16.0/workstation-pro-16-user-guide.pdf>

## Random Knowledge Check: The Difference between Network address & Host Address

Given, Subnet IP 10.10.10.0 and Subnet Mask 255.255.255.0

Can Node A 10.10.11.23/24 ping node B IP 10.10.10.45/24 ?

Why/Why not?

### HINT

An IP address has two components

1. Network Address: Identifies the Network
2. Host Address: Identifies the Host

[Home](/README.md)
[Labs](/labs/labs.md)