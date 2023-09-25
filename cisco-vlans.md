



New Command | what it does
------------|-------------
vlan 33 | creates or edits a vlan
(config-vlan)# name bleh | names a vlan bleh
do sh vlan brief | shows vlan
(config-if)switchport trunk encapsulation dot1q | sets the trunk mode to the modern 802.1q.
(config-if)switchport nonegotiate | disables the trunk mode legacy compatability
(config-if)switchport mode trunk | sets the interface as a trunk, doesn't work on layer 3 switch
(config-if)switchport access vlan 33 | Allows the interface to access vlan 33
(config-if)switchport trunk allowed vlan 33,44,55,63 | allow vlans to cross the trunk link
(config-if)switchport trunk native vlan 888 | sets the native vlan
(config-if)do sh int trunk | shows useful information about the trunk



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
ip default-gateway 172.16.1.0 255.255.255.0
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
int range g1/0/1-8
switchport mode access
switchport access vlan 33
no shut
exit
int range g1/0/9-12
switchport mode access
switchport access vlan 44
no shut
exit
int range g1/0/13-18
switchport mode access
switchport access vlan 55
no shut
exit
int vlan 63
!switchport mode access
!switchport access vlan 63
ip add 172.16.63.0 255.255.255.128
desc ITmgmt
no shut
exit
int g1/0/24
switchport trunk encapsulation dot1q
switchport nonegotiate
switchport mode trunk
switchport trunk allowed vlan 33,44,55,63
switchport trunk native vlan 888
no shut
exit
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
ip default-gateway 172.16.1.0 255.255.255.0
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
int range g1/0/1-6
switchport mode access
switchport access vlan 33
no shut
exit
int range g1/0/7-14
switchport mode access
switchport access vlan 44
no shut
exit
int range g1/0/15-22
switchport mode access
switchport access vlan 55
no shut
exit
int vlan 63
switchport mode access
switchport access vlan 63
ip add 172.16.63.0 255.255.255.128
desc ITmgmt
no shut
exit
int g1/0/23
switchport mode access
switchport access vlan 63
no shut
int g1/0/24
switchport trunk encapsulation dot1q
switchport nonegotiate
switchport mode trunk
switchport trunk allowed vlan 33,44,55,63
switchport trunk native vlan 888
no shut
exit
!copy run start
!show arp
!show run
```

</summary> </details>
