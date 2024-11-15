

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
  <img width="900" height="400" src="https://github.com/tiago-amado/sxr/pics/sxr-clab_physical.png?raw=true">
</p>



The setup contains six SROS FP5 & FP4 routers with 23.10R2 and 2 linux hosts. The network contains 2 P routers, 2 PEs running ANYSec and MACSec, 2 CEs with MACSec, and 2 Linux Clients with 3 interfaces for 3 distinct services. 
Only the PEs have ANYSec configured. The models are:
* 2x SXR nodes 
* 2x Linux hosts with multiple interfaces to ilustrate distinct customers/services



## Logical setup

There are 3 distinct EVPN services: VPWS, MAC-VRF and IP-VRF



<p align="center">
  <img width="900" height="400" src="https://github.com/tiago-amado/sxr/pics/sxr-clab_logical.png?raw=true">
</p>


The setup has:

* ISIS instance 0
* LDP/TLDP
* MP-iBGP (no RR)
* EVPN Services: 1_vpws, 2_mac-vrf and 3_ip-vrf




