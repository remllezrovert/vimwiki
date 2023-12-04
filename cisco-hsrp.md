# Cisco HSRP 
by Trevor Zellmer

## Purpose:
HSRP allows for failover when routers fail. This is useful because it allows for reduncency within networks which helps minimise 
the threat of unforseen outages.

#### Theory:
- HSRP is 'Hot Standby Router Protocol'
- allows multiple routers to appear as one by assigning a virtual IP and matching virtual MAC address
- HSRP elects a single active router and puts the others on standby incase the active router fails
- multiple HSRP groups can be load balenced
- default priority 100

#### New Commands
New Command | what it does
------------|-------------
sh standby brief | display information about hsrp
(config-if) standby version 2 | sets the standy version to the newer version
(config-if) standby 1 preempt | if the router goes offline, when it comes back it will be the main active router
(config-if) standby 1 ip address 192.168.110.1 | assign a virtual address for a standy interface
(config-if) standby 1 priority 150 | boost the priority of a standby router over the default 100.


## Procedure
1. Cable according to diagram

![hsrp](hsrp.png)
![cisco-hsrp-table](cisco-hsrp-table.png)

2. Change r1 because now things are different
- a. Change the ip addresses of each subinterface to end with 2 instead of 1



3. Change r2 because now things are different
- a. Change interface groups on r2 to free up g0/0/0
- b. Change routes on r2 so that traffic destined for upper vlans goes to ALS4 not s0/2/0
- c. Create floating backup routes on r2 so that if r2 can't access ALS4 it will use s0/2/0 instead

4. Change ALS4 because now things are different
- d. Change interface groups on ALS4 to free up G1/0/20
- e. Set up ALS4 g1/0/20 as a vlan trunk for the upper vlans

5. Set up HSRP on R1 for high priority vlan 33 and 44
- a. Edit subinterface: **int g0/0/0.33**
- b. Assign actual ip address: **ip add 192.168.33.2 255.255.255.0**
- c. Enable HSRP: **standby version 2**
- d. Set the virtual HSRP address: **standby 1 ip 192.168.33.1 255.255.255.0**
- e. Make this interface a preffered on failure: **standby 1 priority 150**
- f. After this router recovers from failure, make it the main router: **standby 1 preempt**

6. Set up HSRP on R1 for low priority vlan 55 and 63
- a. Edit subinterface: **int g0/0/0.55**
- b. Assign actual ip address: **ip add 192.168.55.2 255.255.255.0**
- c. Enable HSRP: **standby version 2**
- d. Set the virtual HSRP address: **standby 1 ip 192.168.55.1 255.255.255.0**
- e. After this router recovers from failure, make it the main router: **standby 1 preempt**

7. Configure R2 for HSRP
- a. Set up HSRP for LOW priority on vlan 33 and 44
- b. Set up HSRP for HIGH priority on vlan 55 and 63
- c. See step 6 for more information





Troubleshooting and Verification



1. Set verify HSRP on R1
- a. Verify working configuration: **do sh standby brief**
- b. Disconnect g0/0/0 on R2
- c. Verify failover configuration: **do sh standby brief**
- d. Reconnect the cable
- e. Disconnect g0/0/0 on R1
- f. Verify failover configuration: **do sh standby brief**
- g. Reconnect the cable
- h. Ensure that your output is similar to the output below

![cisco-hsrp-r1](cisco-hsrp-r1.png)


2. Show routes on DLS1 while everything is up
- a. Display information: **do sh route**
- b. Ensure your configuration is similar to the one below

![cisco-hsrp-dls1up](cisco-hsrp-dls1up.png)

3. Show routes on DLS1 while R1's g0/0/1 is down
- a. Disconnect the cable
- b. Display information: **do sh route**
- c. Ensure your configuration is similar to the one below
- d. Reconnect the cable

![cisco-hsrp-dls1-r1down](cisco-hsrp-dls1-r1down.PNG)



4. Show routes on DLS1 while R2's g0/0/1 is down
- a. Disconnect the cable
- b .Display information **do sh route**
- c. Ensure your configuration is similar to the one below
- d. Reconnect the cable

![cisco-hsrp-dls1-r2down](cisco-hsrp-dls1-r2down.PNG)

5. If you cannot figure out what is wrong with a device, wipe it and retype all of the commands.
- a. Enter user exec mode: **en** </br>
- b. Enter global exec mode: **conf t** </br>
- c. Wipe the device to factory settings:  **write erase** </br>
- d. Reboot the device so that the changes take effect: **reload** </br>
- e. Refer to the instructions above for configuring each device on the network.



<details> <summary>Script</summary>


```
! ===============================
! This is switch 1 config
en
config t
hostname ALS1
no ip domain-lookup
line con 0
password cisco login
logging sync
exec-time 120 0
enable secret class
service password-encryption
ip domain name challenge.local
crypto key generate rsa
1024
ip ssh ver 2
username student secret cisco 
username admin priv 15 secret cisco 
line vty 0 15
transport input ssh
login local
banner motd % keep out %
ip default-gateway 
vlan 33
name Sales
exit
vlan 44
name Manufacturing
exit
vlan 55
name Admin
exit
vlan 63
name ITmgmt
exit
vlan 888
name NativeONLY
exit
int range gi1/0/1-8
switchport mode access
switchport access vlan 33
no shut
exit
int range gi1/0/9-12
switchport mode access
switchport access vlan 44
no shut
exit
int range gi1/0/13-18
switchport mode access
switchport access vlan 55
no shut
exit
int vlan 63
ip add 172.16.63.5 255.255.255.128
desc ITmgmt
no shut
exit
int range gi1/0/20-21
shut
channel-group 2 mode desir
int po2
shut
desc connect to ALS4
!switchport trunk encapsulation dot1q
switchport nonegotiate
switchport mode trunk
switchport trunk allowed vlan 33,44,55,63
switchport trunk native vlan 888
no shut
exit
int gi1/0/23
!switchport trunk encapsulation dot1q
switchport nonegotiate
switchport mode trunk
switchport trunk allowed vlan 33,44,55,63
switchport trunk native vlan 888
no shut
exit
int range gi1/0/24, gi1/0/22
shut
channel-group 1 mode active
int po1
shut
!switchport trunk encapsulation dot1q
switchport nonegotiate
switchport mode trunk
switchport trunk allowed vlan 33,44,55,63
switchport trunk native vlan 888
no shut
exit
spanning-tree mode rapid-pvst
spanning-tree portfast default
spanning-tree portfast bpduguard default
spanning-tree vlan 33 root primary
spanning-tree vlan 44 root primary
spanning-tree vlan 55 root secondary
spanning-tree vlan 63 root secondary
ip access-list standard BlockSales
 remark Block R1 Sales network
 deny   172.16.33.0 0.0.0.255
 remark Block 3750-2 Sales network
 deny   172.16.128.0 0.0.0.255
 permit any
line vty 0 15
 access-class BlockSales in
!copy run start
!show arp
!show run


! ===============================
! This is switch 2 config
en
config t
hostname ALS2
no ip domain-lookup
line con 0
password cisco
login
logging sync
exec-time 120 0
enable secret class
service password-encryption
ip domain name challenge.local
crypto key generate rsa
1024
ip ssh ver 2
username student secret cisco 
username admin priv 15 secret cisco
line vty 0 15
transport input ssh
login local
banner motd % keep out %
ip default-gateway 
vlan 33
name Sales
exit
vlan 44
name Manufacturing
exit
vlan 55
name Admin
exit
vlan 63
name ITmgmt
exit
vlan 888
name NativeONLY
exit
int range gi1/0/1-6
switchport mode access
switchport access vlan 33
no shut
exit
int range gi1/0/7-14
switchport mode access
switchport access vlan 44
no shut
exit
int range gi1/0/15-18
switchport mode access
switchport access vlan 55
no shut
exit
int vlan 63
ip add 172.16.63.6 255.255.255.128
desc ITmgmt
no shut
exit
int range gi1/0/23-24
shut
channel-group 1 mode active
int po1
shut
!switchport trunk encapsulation dot1q
switchport nonegotiate
switchport mode trunk
switchport trunk allowed vlan 33,44,55,63
switchport trunk native vlan 888
no shut
exit
int range gi1/0/21-22
shut
channel-group 2 mode active
int po2
shut
desc Connect to ALS4
!switchport trunk encapsulation dot1q
switchport nonegotiate
switchport mode trunk
switchport trunk allowed vlan 33,44,55,63
switchport trunk native vlan 888
no shut
exit
spanning-tree mode rapid-pvst
spanning-tree portfast default
spanning-tree portfast bpduguard default
ip access-list standard BlockSales
 remark Block R1 Sales network
 deny   172.16.33.0 0.0.0.255
 remark Block 3750-2 Sales network
 deny   172.16.128.0 0.0.0.255
 permit any
line vty 0 15
 access-class BlockSales in
!sh ip trunk brief
!sh vlan brief
!copy run start
!show arp
!show run

! ===============================
! This is ALS3 config
en
config t
hostname ALS3
no ip domain-lookup
line con 0
password cisco
login
logging sync
exec-time 120 0
enable secret class
service password-encryption
ip domain name challenge.local
crypto key generate rsa
1024
ip ssh ver 2
username student secret cisco 
username admin priv 15 secret cisco
line vty 0 15
transport input ssh
login local
banner motd % keep out %
ip default-gateway 172.16.153.1
vlan 128
name Sales
exit
vlan 138
name Manufacturing
exit
vlan 148
name Admin
exit
vlan 153
name ITmgmt
exit
vlan 999
name NativeONLY
exit
int range gi1/0/1-8
switchport mode access
switchport access vlan 128
no shut
exit
int range gi1/0/9-12
switchport mode access
switchport access vlan 138
no shut
exit
int range gi1/0/13-18
switchport mode access
switchport access vlan 148
no shut
exit
int vlan 153
ip add 172.16.153.6 255.255.255.128
desc ITmgmt
no shut
exit
int range gi1/0/23-24
shut
channel-group 1 mode desir
int po1
shut
desc Connect to DLS1
!sdm prefer dual-ipv4-and-ipv6 default
!switchport trunk encapsulation dot1q
switchport nonegotiate
switchport mode trunk
switchport trunk allowed vlan 128,138,148,153
switchport trunk native vlan 999
no shut
exit
spanning-tree mode rapid-pvst
spanning-tree portfast default
spanning-tree portfast bpduguard default
ip access-list standard BlockSales
 remark Block R1 Sales network
 deny   172.16.33.0 0.0.0.255
 remark Block 3750-2 Sales network
 deny   172.16.128.0 0.0.0.255
 permit any
line vty 0 15
 access-class BlockSales in
!sh ip trunk brief
!sh vlan brief
!copy run start
!show arp
!show run


! ===============================
! This is switch 4 config
en
config t
hostname ALS4
no ip domain-lookup
line con 0
password cisco
login
logging sync
exec-time 120 0
enable secret class
service password-encryption
ip domain name challenge.local
crypto key generate rsa
1024
ip ssh ver 2
username student secret cisco 
username admin priv 15 secret cisco
line vty 0 15
transport input ssh
login local
banner motd % keep out %
ip default-gateway 
vlan 33
name Sales
exit
vlan 44
name Manufacturing
exit
vlan 55
name Admin
exit
vlan 63
name ITmgmt
exit
vlan 888
name NativeONLY
exit
int range gi1/0/1-6
switchport mode access
switchport access vlan 33
no shut
exit
int range gi1/0/7-14
switchport mode access
switchport access vlan 44
no shut
exit
int range gi1/0/15-18
switchport mode access
switchport access vlan 55
no shut
exit
int vlan 63
ip add 172.16.63.7 255.255.255.128
desc ITmgmt
no shut
exit
int range gi1/0/23-24
shut
channel-group 1 mode desir
int po1
shut
desc Connect to ALS1
!switchport trunk encapsulation dot1q
switchport nonegotiate
switchport mode trunk
switchport trunk allowed vlan 33,44,55,63
switchport trunk native vlan 888
no shut
exit
int range gi1/0/21-22
shut
channel-group 2 mode active
int po2
shut
desc Connect to ALS2
!switchport trunk encapsulation dot1q
switchport nonegotiate
switchport mode trunk
switchport trunk allowed vlan 33,44,55,63
switchport trunk native vlan 888
no shut
exit
int g1/0/20
shut
desc Connect to R2
switchport nonegotiate
switchport mode trunk
switchport trunk allowed vlan 33,44,55,63
switchport trunk native vlan 888
no shut
exit
spanning-tree mode rapid-pvst
spanning-tree portfast default
spanning-tree portfast bpduguard default
spanning-tree vlan 63 root primary
spanning-tree vlan 55 root primary
spanning-tree vlan 33 root secondary
spanning-tree vlan 44 root secondary
ip access-list standard BlockSales
 remark Block R1 Sales network
 deny   172.16.33.0 0.0.0.255
 remark Block 3750-2 Sales network
 deny   172.16.128.0 0.0.0.255
 permit any
line vty 0 15
 access-class BlockSales in
!sh ip trunk brief
!sh vlan brief
!copy run start
!show arp
!show run




! ===============================
! This is DLS1 config
en
config t
hostname DLS1
no ip domain-lookup
line con 0
password cisco
login
logging sync
exec-time 120 0
enable secret class
service password-encryption
ip domain name challenge.local
crypto key generate rsa
1024
ip ssh ver 2
username student secret cisco 
username admin priv 15 secret cisco
line vty 0 15
transport input ssh
login local
banner motd % keep out %
ip default-gateway 172.254.0.1
ip routing
!sdm prefer dual-ipv4-and-ipv6 default
ipv6 unicast-routing
do copy run start
vlan 138
name Sales
exit
vlan 138
name Manufacturing
vlan 148
name Admin
vlan 153
name ITmgmt
vlan 999
name NativeONLY
exit
int vlan 128
ip add 172.16.128.1 255.255.255.0
ipv6 add 2001:db8:ffff:d0::1/64
ipv6 add FE80::A link-local
ip helper-address 192.168.150.1
exit
int vlan 138
ip add 172.16.138.1 255.255.255.0
ipv6 add 2001:db8:ffff:d1::1/64
ipv6 add FE80::A link-local
ip helper-address 192.168.150.1
exit
int vlan 148
ip add 172.16.148.1 255.255.255.0
ipv6 add 2001:db8:ffff:d2::1/64
ipv6 add FE80::A link-local
ip helper-address 192.168.150.1
exit
int vlan 153
ip add 172.16.153.1 255.255.255.0
ip helper-address 192.168.150.1
exit
int range gi1/0/1-8
switchport mode access
switchport access vlan 128
no shut
exit
int range gi1/0/9-12
switchport mode access
switchport access vlan 138
no shut
exit
int range gi1/0/13-18
switchport mode access
switchport access vlan 148
no shut
exit
int gi1/0/22
no switchport
ip add 172.254.0.6 255.255.255.252
ipv6 add 2001:db8:ffff:2::6/64
ipv6 add FE80::A link-local
no shut
int gi1/0/23
no switchport
ip add 172.254.0.2 255.255.255.252
ipv6 add 2001:db8:ffff:1::2/64
ipv6 add FE80::A link-local
no shut
int vlan 153
ip add 172.16.153.1 255.255.255.128
desc ITmgmt
no shut
exit
int range gi1/0/21, gi1/0/24
shut
channel-group 1 mode desir
int po1
shut
desc Connect to ALS3
!switchport trunk encapsulation dot1q
switchport nonegotiate
switchport mode trunk
switchport trunk allowed vlan 128,138,148,153
switchport trunk native vlan 999
no shut
exit
!sh ip trunk brief
!sh vlan brief
!copy run start
!show arp
!show run
!Step 6a & b
ip route 172.16.33.0 255.255.255.0 172.254.0.1
ipv6 route 2001:db8:ffff:c0::/64 2001:db8:ffff:1::1
ip route 172.16.33.0 255.255.255.0 172.254.0.5 16
ipv6 route 2001:db8:ffff:c0::/64 2001:db8:ffff:2::5 16
ip route 172.16.44.0 255.255.255.0 172.254.0.1
ipv6 route 2001:db8:ffff:c1::/64 2001:db8:ffff:1::1
ip route 172.16.44.0 255.255.255.0 172.254.0.5 16
ipv6 route 2001:db8:ffff:c1::/64 2001:db8:ffff:2::5 16
ip route 172.16.55.0 255.255.255.0 172.254.0.5
ipv6 route 2001:db8:ffff:c2::/64 2001:db8:ffff:1::1
ip route 172.16.55.0 255.255.255.0 172.254.0.1 16
ipv6 route 2001:db8:ffff:c2::/64 2001:db8:ffff:2::5 16
ip route 172.16.63.0 255.255.255.0 172.254.0.5
ip route 172.16.63.0 255.255.255.0 172.254.0.1 16
!Step 6c & d
ip route 172.254.0.8 255.255.255.252 172.254.0.1
ipv6 route 2001:db8:ffff:3::/64 2001:db8:ffff:1::1
ip route 172.254.0.8 255.255.255.252 172.254.0.5 32
ipv6 route 2001:db8:ffff:3::/64 2001:db8:ffff:2::5 32
!Step 6e & f
ip route 192.168.150.1 255.255.255.255 172.254.0.1
ipv6 route 2001:db8:acad:0::1/128 2001:db8:ffff:1::1
ip route 192.168.150.1 255.255.255.255 172.254.0.5 64
ipv6 route 2001:db8:acad:0::1/128 2001:db8:ffff:2::5 64
spanning-tree mode rapid-pvst
spanning-tree portfast default
spanning-tree portfast bpduguard default
ip access-list standard BlockSales
spanning-tree vlan 128 root primary
spanning-tree vlan 138 root primary
spanning-tree vlan 148  root primary 
spanning-tree vlan 153 root primary
ip access-list standard BlockSales
 remark Block R1 Sales network
 deny   172.16.33.0 0.0.0.255
 remark Block 3750-2 Sales network
 deny   172.16.128.0 0.0.0.255
 permit any
line vty 0 15
 access-class BlockSales in
ipv6 access-list BlockV6Sales
 remark Block R1 Sales IPv6 network
 deny   ipv6 2001:db8:ffff:c0::/64 any
 remark Block 3750-2 IPv6 network
 deny   ipv6 2001:db8:ffff:d0::/64 any
 permit ipv6 any any
line vty 0 15
 ipv6 access-class BlockV6Sales in
int vlan 128
ipv6 nd prefix default no-autoconfig
ipv6 nd managed-config-flag
ipv6 dhcp relay destination 2001:db8:acad:0::1
int vlan 138
ipv6 nd prefix default no-autoconfig
ipv6 nd managed-config-flag
ipv6 dhcp relay destination 2001:db8:acad:0::1
int vlan 148
ipv6 nd prefix default no-autoconfig
ipv6 nd managed-config-flag
ipv6 dhcp relay destination 2001:db8:acad:0::1
exit


! ================================
! This is router 1 config
en
config t
hostname R1
no ip domain-lookup
line con 0
password cisco
login
logging sync
enable secret class
service password-encryption
ip domain name challenge.local
crypto key generate rsa
1024
ip ssh ver 2
username student secret cisco
username admin priv 15 secret cisco
line vty 0 15
transport input ssh
login local
banner motd % keep out %
! commands below this point are unqiue to routers
line aux 0
password cisco
login
ipv6 unicast-routing
!-- Make Subinterfaces
int gi0/0/0.33
encapsulation dot1q 33
ip address 172.16.33.2 255.255.255.0
standby version 2
standby 1 ip 172.16.33.1
standby 1 priority 150
standby preempt
ipv6 add 2001:db8:ffff:c0::1/64
ipv6 add FE80::1 link-local
int gi0/0/0.44
encapsulation dot1q 44
ip add 172.16.44.2 255.255.255.0
standby version 2
standby 1 ip 172.16.44.1
standby 1 priority 150
standby preempt
ipv6 add 2001:db8:ffff:c0::1/64
ipv6 add 2001:db8:ffff:c1::1/64
ipv6 add FE80::1 link-local
int gi0/0/0.55
encapsulation dot1q 55
ip address 172.16.55.2 255.255.255.0
standby version 2
standby 1 ip 172.16.55.1
standby preempt
ipv6 add 2001:db8:ffff:c0::1/64
ipv6 add 2001:db8:ffff:c2::1/64
ipv6 add FE80::1 link-local
int gi0/0/0.63
encapsulation dot1q 63
ip address 172.16.63.2 255.255.255.0
standby version 2
standby 1 ip 172.16.63.1
standby preempt
ipv6 add FE80::1 link-local
int gi0/0/0
desc Connect to ALS1
no shut
int gi0/0/1
desc Connect to DLS1
ip add 172.254.0.1 255.255.255.252
ipv6 add 2001:db8:ffff:1::1/64
ipv6 add FE80::1 link-local
no shut
int s0/2/0
desc Connect to R2
ip add 172.254.0.9 255.255.255.252
ipv6 add 2001:db8:ffff:3::9/64
ipv6 add FE80::1 link-local
no shut
int Lo0
desc Loopback 0
ip add 192.168.150.1 255.255.255.255
ipv6 add 2001:db8:acad:0::1/128
ipv6 add FE80::1 link-local
no shut
exit
!Step 5a & b
ip route 172.16.128.0 255.255.255.0 172.254.0.2
ipv6 route 2001:db8:ffff:d0::/64 2001:db8:ffff:1::2 
ip route 172.16.128.0 255.255.255.0 172.254.0.10 16
ipv6 route 2001:db8:ffff:d0::/64 2001:db8:ffff:3::A 16
ip route 172.16.138.0 255.255.255.0 172.254.0.2
ipv6 route 2001:db8:ffff:d1::/64 2001:db8:ffff:1::2
ip route 172.16.138.0 255.255.255.0 172.254.0.10 16
ipv6 route 2001:db8:ffff:d1::/64 2001:db8:ffff:3::A 16
ip route 172.16.148.0 255.255.255.0 172.254.0.2
ipv6 route 2001:db8:ffff:d2::/64 2001:db8:ffff:1::2
ip route 172.16.148.0 255.255.255.0 172.254.0.10 16
ipv6 route 2001:db8:ffff:d2::/64 2001:db8:ffff:3::A 16
ip route 172.16.153.0 255.255.255.128 172.254.0.2
ip route 172.16.153.0 255.255.255.128 172.254.0.10 16
!Step 5c & d
ip route 172.254.0.4 255.255.255.252 172.254.0.2
ipv6 route 2001:db8:ffff:2::/64 2001:db8:ffff:1::2
ip route 172.254.0.4 255.255.255.252 172.254.0.10 32
ipv6 route 2001:db8:ffff:2::/64 2001:db8:ffff:3::A 32
ip route 172.16.33.0 255.255.255.0 172.254.0.10 24
ip route 172.16.44.0 255.255.255.0 172.254.0.10 24
ip route 172.16.55.0 255.255.255.0 172.254.0.10 24
ip route 172.16.63.0 255.255.255.128 172.254.0.10 24
ipv6 route 2001:db8:ffff:c0::/64 2001:db8:ffff:3::A 24
ipv6 route 2001:db8:ffff:c1::/64 2001:db8:ffff:3::A 24
ipv6 route 2001:db8:ffff:c2::/64 2001:db8:ffff:3::A 24
spanning-tree mode rapid-pvst
spanning-tree portfast default
spanning-tree portfast bpduguard default
ip access-list standard BlockSales
 remark Block R1 Sales network
 deny   172.16.33.0 0.0.0.255
 remark Block 3750-2 Sales network
 deny   172.16.128.0 0.0.0.255
 permit any 
 line vty 0 15
 access-class BlockSales in
ipv6 access-list BlockV6Sales
 remark Block R1 Sales IPv6 network
 deny   ipv6 2001:db8:ffff:c0::/64 any
 remark Block 3750-2 IPv6 network
 deny   ipv6 2001:db8:ffff:d0::/64 any
 permit ipv6 any any
line vty 0 15
 ipv6 access-class BlockV6Sales in
ip dhcp excluded-address 172.16.33.0
ip dhcp pool Sales
default-router 
DNS-server 8.8.8.8
domain-name challenge.local
lease 0 6
network 172.16.33.0 255.255.255.0
ip dhcp excluded-address 192.168.128.1 192.168.128.10
ip dhcp pool Sales2
default-router 172.16.128.1
DNS-server 8.8.8.8
domain-name challenge.local
lease 0 6
network 172.16.128.0 255.255.255.0
ipv6 dhcp pool Sales16
address prefix 2001:db8:ffff:c0::/64
dns-server 2001:4860:4860::8888
domain-name challenge.local
int gi0/0/0.33
ipv6 dhcp server Sales16
ipv6 nd prefix default no-autoconfig
exit
ipv6 dhcp pool Sales26
address prefix 2001:db8:ffff:d0::/64
dns-server 2001:4860:4860::8888
domain-name challenge.local
ip dhcp excluded-address 172.16.44.0 172.16.44.10
ip dhcp pool Manufacturing
default-router 172.16.44.1
DNS-server 8.8.8.8
domain-name challenge.local
network 172.16.44.0 255.255.255.0
ip dhcp excluded-address 172.16.138.0 172.16.138.10
ip dhcp pool Manufacturing2
default-router 172.16.138.1
DNS-server 8.8.8.8
domain-name challenge.local
network 172.16.138.0 255.255.255.0
ipv6 dhcp pool Manufacturing16
address prefix 2001:db8:ffff:c1::/64
dns-server 2001:4860:4860::8888
domain-name challenge.local
int gi0/0/0.44
ipv6 dhcp server Manufacturing16
ipv6 nd prefix default no-autoconfig
exit
ipv6 dhcp pool Manufacturing26
address prefix 2001:db8:ffff:d1::/64
dns-server 2001:4860:4860::8888
domain-name challenge.local
ip dhcp excluded-address 172.16.55.0 172.16.55.10
ip dhcp pool Admin
default-router 172.16.55.1
DNS-server 8.8.8.8
domain-name challenge.local
network 172.16.55.0 255.255.255.0
ip dhcp excluded-address 172.16.148.0 172.16.148.10
ip dhcp pool Admin2
default-router 172.16.148.1
DNS-server 8.8.8.8
domain-name challenge.local
network 172.16.148.0 255.255.255.0
ipv6 dhcp pool Admin16
address prefix 2001:db8:ffff:c2::/64
dns-server 2001:4860:4860::8888
domain-name challenge.local
int g0/0/0.55
ipv6 dhcp server Admin16
ipv6 nd prefix default no-autoconfig
exit
ipv6 dhcp pool Admin26
address prefix 2001:db8:ffff:d2::/64
dns-server 2001:4860:4860::8888
domain-name challenge.local
ip dhcp excluded-address 172.16.63.0
ip dhcp pool ITmgmt
default-router 
DNS-server 8.8.8.8
domain-name challenge.local
network 172.16.63.0 255.255.255.128
ip dhcp excluded-address 172.16.153.1 172.16.153.10
ip dhcp pool ITmgmt2
default-router 172.16.153.1
DNS-server 8.8.8.8
domain-name challenge.local
network 172.16.153.0 255.255.255.128
int g0/0/1
ipv6 dhcp server automatic 
int s0/2/0
ipv6 dhcp server automatic 

! ================================
! This is router 2 config
en
config t
hostname R2
no ip domain-lookup
line con 0
password cisco
login
logging sync
enable secret class
service password-encryption
ip domain name challenge.local
crypto key generate rsa
1024
ip ssh ver 2
username student secret cisco
username admin priv 15 secret cisco
line vty 0 15
transport input ssh
login local
banner motd % keep out %
! commands below this point are unqiue to routers
line aux 0
password cisco
login
ipv6 unicast-routing
int s0/2/0
desc Connect to R1
ip add 172.254.0.10 255.255.255.252
ipv6 add 2001:db8:ffff:3::A/64
ipv6 add FE80::2 link-local
no shut
int gi0/0/1
desc Connect to DLS1
ip add 172.254.0.5 255.255.255.252
ipv6 add 2001:db8:ffff:2::5/64
ipv6 add FE80::2 link-local
no shut
exit
int gi0/0/0.33
encapsulation dot1q 33
ip address 172.16.33.3 255.255.255.0
standby version 2
standby 1 ip 172.16.33.1
standby 1 preempt
ipv6 add 2001:db8:ffff:c0::3/64
ipv6 add FE80::2 link-local
ip helper-address 192.168.150.1
ipv6 nd prefix default no-autoconfig
ipv6 nd managed-config-flag
ipv6 dhcp relay destination 2001:db8:acad:0::1
int gi0/0/0.44
encapsulation dot1q 44
ip add 172.16.44.3 255.255.255.0
standby version 2
standby 1 ip 172.16.44.1
standby 1 preempt
ipv6 add 2001:db8:ffff:c1::3/64
ipv6 add FE80::2 link-local
ip helper-address 192.168.150.1
ipv6 nd prefix default no-autoconfig
ipv6 nd managed-config-flag
ipv6 dhcp relay destination 2001:db8:acad:0::1
int gi0/0/0.55
encapsulation dot1q 55
ip address 172.16.55.3 255.255.255.0
standby version 2
standby 1 ip 172.16.55.1
standby 1 priority 150
standby 1 preempt
ipv6 add 2001:db8:ffff:c2::3/64
ipv6 add FE80::2 link-local
ip helper-address 192.168.150.1
ipv6 nd prefix default no-autoconfig
ipv6 nd managed-config-flag
ipv6 dhcp relay destination 2001:db8:acad:0::1
int gi0/0/0.63
encapsulation dot1q 63
ip address 172.16.63.3 255.255.255.0
standby version 2
standby 1 ip 172.16.63.1
standby 1 priority 150
standby 1 preempt
ipv6 add FE80::2 link-local
ip helper-address 192.168.150.1
ipv6 nd prefix default no-autoconfig
ipv6 nd managed-config-flag
ipv6 dhcp relay destination 2001:db8:acad:0::1
int gi0/0/0
desc Connect to ALS4
no shut
!Step 7a & b
ip route 172.16.33.0 255.255.255.0 172.254.0.9
ipv6 route 2001:db8:ffff:c0::/64 2001:db8:ffff:3::9
ip route 172.16.33.0 255.255.255.0 172.254.0.6 16
ipv6 route 2001:db8:ffff:c0::/64 2001:db8:ffff:2::6 16
ip route 172.16.44.0 255.255.255.0 172.254.0.9
ipv6 route 2001:db8:ffff:c1::/64 2001:db8:ffff:3::9
ip route 172.16.44.0 255.255.255.0 172.254.0.6 16
ipv6 route 2001:db8:ffff:c1::/64 2001:db8:ffff:2::6 16
ip route 172.16.55.0 255.255.255.0 172.254.0.9
ipv6 route 2001:db8:ffff:c2::/64 2001:db8:ffff:3::9
ip route 172.16.55.0 255.255.255.0 172.254.0.6 16
ipv6 route 2001:db8:ffff:c2::/64 2001:db8:ffff:2::6 16
ip route 172.16.63.0 255.255.255.0 172.254.0.9
ip route 172.16.63.0 255.255.255.0 172.254.0.6 16
!Step 7c & d
ip route 172.16.128.0 255.255.255.0 172.254.0.6
ipv6 route 2001:db8:ffff:d0::/64 2001:db8:ffff:2::6
ip route 172.16.128.0 255.255.255.0 172.254.0.9 16
ipv6 route 2001:db8:ffff:d0::/64 2001:db8:ffff:3::9 16
ip route 172.16.138.0 255.255.255.0 172.254.0.6
ipv6 route 2001:db8:ffff:d1::/64 2001:db8:ffff:2::6
ip route 172.16.138.0 255.255.255.0 172.254.0.9 16
ipv6 route 2001:db8:ffff:d1::/64 2001:db8:ffff:3::9 16
ip route 172.16.148.0 255.255.255.0 172.254.0.6
ipv6 route 2001:db8:ffff:d2::/64 2001:db8:ffff:2::6
ip route 172.16.148.0 255.255.255.0 172.254.0.9 16
ipv6 route 2001:db8:ffff:d2::/64 2001:db8:ffff:3::9 16
ip route 172.16.153.0 255.255.255.128 172.254.0.6
ip route 172.16.153.0 255.255.255.128 172.254.0.9 16
!Step 7e & f
ip route 172.254.0.0 255.255.255.252 172.254.0.6
ipv6 route 2001:db8:ffff:1::/64 2001:db8:ffff:2::6
ip route 172.254.0.0 255.255.255.252 172.254.0.9 32
ipv6 route 2001:db8:ffff:1::/64 2001:db8:ffff:3::9 32
!Step 7g & h
ip route 192.168.150.1 255.255.255.255 172.254.0.9
ipv6 route 2001:db8:acad:0::1/128 2001:db8:ffff:3::9
ip route 192.168.150.1 255.255.255.255 172.254.0.6 64
ipv6 route 2001:db8:acad:0::1/128 2001:db8:ffff:2::6 64
!------ hsrp ------------------------------------------
ip route 172.16.33.0 255.255.255.0 172.254.0.7 24
ip route 172.16.44.0 255.255.255.0 172.254.0.7 24
ip route 172.16.55.0 255.255.255.0 172.254.0.7 24
ip route 172.16.63.0 255.255.255.128 172.254.0.7 24
ipv6 route 2001:db8:ffff:c0::/64 2001:db8:ffff:1::7 24
ipv6 route 2001:db8:ffff:c1::/64 2001:db8:ffff:1::7 24
ipv6 route 2001:db8:ffff:c2::/64 2001:db8:ffff:1::7 24
spanning-tree mode rapid-pvst
spanning-tree portfast default
spanning-tree portfast bpduguard default
ip access-list standard BlockSales
 remark Block R1 Sales network
 deny   172.16.33.0 0.0.0.255
 remark Block 3750-2 Sales network
 deny   172.16.128.0 0.0.0.255
 permit any
line vty 0 15
 access-class BlockSales in
 ipv6 access-list BlockV6Sales
 remark Block R1 Sales IPv6 network
 deny   ipv6 2001:db8:ffff:c0::/64 any
 remark Block 3750-2 IPv6 network
 deny   ipv6 2001:db8:ffff:d0::/64 any
 permit ipv6 any any
line vty 0 15
 ipv6 access-class BlockV6Sales in
```

</summary> </details>
