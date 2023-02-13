# Virtual Network: Virtual LAN Router 

## Apply what you've learned
### Challenge: Test Connectivity
- Create & Configure the LAN router
- Create and Configure two VMs one for the DMZ and the other for LOCAL LAN
- Use your VM's to ping from the the 10.0.1.0/24 network (DMZ) to the 192.168.1.0/24 (Local LAN)  

## Required Changes VyOS
- [ ] Virutal Machine Hardware
- Network Adapter: LAN Segment (LAN1)
- Network Adapter 2: LAN Segment (LOCAL LAN)
- [ ] VyOS Configuration
- eth0 = DHCP
- eth1 = 192.168.1.1
#### Tip
- Using multiple VMs can be helpful when test connectivity <br>
<br> <img src="lan.PNG"> <br>
### Good Luck
<img src="hint.gif"> <br>
- We'll Go over any questions/issues during our alloted time
### References:
- [ ] https://vyos.io/solutions/vyos-on-vmware
- [ ] [User Guide](https://docs.vyos.io/en/latest/index.html)
- [ ] [User Guide: Quick Start](https://docs.vyos.io/en/latest/quick-start.html)
- [ ] Alternative Resources: VyOS Cheat Sheet 
- https://github.com/bertvv/cheat-sheets/blob/master/docs/VyOS.md

## Troubleshooting steps
- [ ] Restart VM
- [ ] Verify VyOS configuration `show config`
- [ ] Verify VyOs interfaces `show interfaces`
- [ ] Verify network adapter on VMware
- [ ] Reference Documentation and Resources 

