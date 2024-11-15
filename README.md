

# SXR Basic lab setup
This is a basic setup with some basic configurations:
* Underlay transport configs: Interfaces, LAG, IPv4, ISIS, LDP, MP-iBGP
* Overlay EVPN services: VPWS, MAC-VRF and IP-VRF

The Nokia SRLinux 7730 SXR FPCx based were introduced as Beta in SRL 24.7.R2 and GA in 24.10R1.
Currently only sxr1x44s and sxr1d32d are available. Other models will be released in R25 and R26. 


## Requirements 

To deploy this lab you need a server with Docker and CLAB and Internet connectivity.
You need to use SRLinux R24 or above Image and a valid License file under /opt/nokia/sros/srl_r24_license.key. 
Note: Despite this is SRLinux a license is required for the 7730SXR nodes.



## Clone and deploy the git lab on your server

To deploy this lab, you must clone it to your server with "git clone".

```bash
# change to your working directory
cd /home/user/
# Clone the lab to your server
git clone https://github.com/tiago-amado/sxr.git
```

## Physical setup

The physical setup is ilustrated below:



<p align="center">
  <img width="900" height="400" src="https://github.com/tiago-amado/sxr/blob/main/pics/sxr-clab_physical.png">
</p>



The setup contains six SROS FP5 & FP4 routers with 23.10R2 and 2 linux hosts. The network contains 2 P routers, 2 PEs running ANYSec and MACSec, 2 CEs with MACSec, and 2 Linux Clients with 3 interfaces for 3 distinct services. 
Only the PEs have ANYSec configured. The models are:
* 2x SXR nodes 
* 2x Linux hosts with multiple interfaces to ilustrate distinct customers/services



## Logical setup

There are 3 distinct EVPN services: VPWS, MAC-VRF and IP-VRF



<p align="center">
  <img width="900" height="400" src="https://github.com/tiago-amado/sxr/blob/main/pics/sxr-clab_logical.png">
</p>


The setup has:

* ISIS instance 0
* LDP/TLDP
* MP-iBGP (no RR)
* EVPN Services: 1_vpws, 2_mac-vrf and 3_ip-vrf


## Test the setup

Test the setup by starting an ICMP from host1 towards host2 on all interfaces:
```bash
ping 192.168.51.2
ping 192.168.52.2   ## you may need to start an icmp on host 2 to trigger an arp to the EVPN
ping 192.168.63.2   ## distint subnets on each host
```


To clear the arps use the following commands
```bash
# at both hosts
ip -s -s neigh flush all

#at both sxr:
/tools network-instance 2_mac-vrf bridge-table mac-learning delete-all-macs
/tools network-instance 2_mac-vrf bridge-table proxy-arp dynamic delete-all
/tools network-instance 2_mac-vrf bridge-table mac-learning learnt-entries mac <HOST-MAC> delete-mac

#view the Macs
/show network-instance 2_mac-vrf bridge-table mac-table all
```


You may perform additional validations on each host and SRX node by using shows or info from state for each service.


