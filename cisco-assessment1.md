
by Trevor Zellmer

<details> <summary>Script</summary>


```
! ===============================
! This is switch 1 config
en
config t
hostname ALS1
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
ip default-gateway 172.131.0.1
vlan 119
name Students
exit
vlan 128
name Faculty
exit
vlan 131
name ITmgmt
exit
vlan 1000
name NativeONLY
exit
int range gi1/0/6-12
switchport mode access
switchport access vlan 119
no shut
exit
int range gi1/0/13-24
switchport mode access
switchport access vlan 128
no shut
exit
int vlan 131
ip add 172.131.0.2 255.255.255.240
desc ITmgmt
no shut
exit
int gi1/0/1
!switchport trunk encapsulation dot1q
desc Trunk to ALS2
switchport nonegotiate
switchport mode trunk
switchport trunk allowed vlan 119,128,131
switchport trunk native vlan 
no shut
exit
int gi1/0/5
!switchport trunk encapsulation dot1q
desc trunk to R1
switchport nonegotiate
switchport mode trunk
switchport trunk allowed vlan 119,128,131
switchport trunk native vlan 1000 
no shut
exit
spanning-tree mode rapid-pvst
spanning-tree portfast default
spanning-tree portfast bpduguard default
spanning-tree vlan 119 root primary
spanning-tree vlan 128 root primary
spanning-tree vlan 131 root primary
ip access-list standard BlockStudents
 remark Block R1 Students network
 deny   172.119.0.0 0.0.0.255
 remark Block 3750-2 Students network
 deny   172.128.0.0 0.0.0.255
 permit any
line vty 0 15
 access-class BlockStudents in
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
ip default-gateway 172.131.0.1
vlan 119
name Students
exit
vlan 128
name Faculty
exit
vlan 131
name ITmgmt
exit
vlan 1000
name NativeONLY
exit
int range gi1/0/6-12
switchport mode access
switchport access vlan 119
no shut
exit
int range gi1/0/13-24
switchport mode access
switchport access vlan 128
no shut
exit
exit
int vlan 131
ip add 172.131.0.3 255.255.255.240
desc ITmgmt
no shut
exit
int gi1/0/1
desc Trunk to ALS1
!switchport trunk encapsulation dot1q
switchport nonegotiate
switchport mode trunk
switchport trunk allowed vlan 119,128,131
switchport trunk native vlan 1000
no shut
exit
spanning-tree mode rapid-pvst
spanning-tree portfast default
spanning-tree portfast bpduguard default
ip access-list standard BlockStudents
 remark Block R1 Students network
 deny   172.119.0.0 0.0.0.255
 remark Block 3750-2 Students network
 deny   172.128.0.0 0.0.0.255
 permit any
line vty 0 15
 access-class BlockStudents in
!sh ip trunk brief
!sh vlan brief
!copy run start
!show arp
!show run

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
int gi0/0/0
ip address 172.18.0.1 255.255.255.252
int gi0/0/1.119
encapsulation dot1q 119
ip address 172.119.0.1 255.255.255.128
int gi0/0/1.128
encapsulation dot1q 128
ip add 172.128.0.1 255.255.255.0
int gi0/0/1.131
encapsulation dot1q 131
ip address 172.131.0.1 255.255.255.240
int gi0/0/1
desc Connect to ALS1
no shut
int gi0/0/1
exit
int Lo0
desc Loopback 0
ip add 10.10.10.1 255.255.255.0
no shut
exit
!Step 5a & b
spanning-tree mode rapid-pvst
spanning-tree portfast default
spanning-tree portfast bpduguard default
ip access-list standard BlockStudents
 remark Block R1 Students network
 deny   172.119.0.0 0.0.0.255
 remark Block 3750-2 Students network
 deny   172.128.0.0 0.0.0.255
 permit any
line vty 0 15
 access-class BlockStudents in
ipv6 access-list BlockV6Students
 remark Block R1 Students IPv6 network
 deny   ipv6 2001:db8:ffff:c0::/64 any
 remark Block 3750-2 IPv6 network
 deny   ipv6 2001:db8:ffff:d0::/64 any
 permit ipv6 any any
line vty 0 15
 ipv6 access-class BlockV6Students in

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
int gi0/0/0
ip address 172.18.0.2 255.255.255.252
line aux 0
password cisco
login
ipv6 unicast-routing
ip route 0.0.0.0 255.255.255.0 172.18.0.2
spanning-tree mode rapid-pvst
spanning-tree portfast default
spanning-tree portfast bpduguard default
ip access-list standard BlockStudents
 remark Block R1 Students network
 deny   172.119.0.0 0.0.0.255
 remark Block 3750-2 Students network
 deny   172.128.0.0 0.0.0.255
 permit any
line vty 0 15
 access-class BlockStudents in
 ipv6 access-list BlockV6Students
 remark Block R1 Students IPv6 network
 deny   ipv6 2001:db8:ffff:c0::/64 any
 remark Block 3750-2 IPv6 network
 deny   ipv6 2001:db8:ffff:d0::/64 any
 permit ipv6 any any
line vty 0 15
 ipv6 access-class BlockV6Students in
```

</summary> </details>
