




<details> <summary>DHCP Server</summary>

```
en
config t
hostname DHCP
no ip domain-lookup
line con 0
password cisco
login
logging sync
enable secret class
service password-encryption
ip domain name k12.local
crypto key generate rsa
1024
ip ssh ver 2
username student secret cisco
username admin priv 15 secret cisco
line vty 0 15
transport input ssh
login local
banner motd % keep out %
ip default-gateway 10.200.1.150.1
! commands below this point are unqiue to routers
line aux 0
password cisco
login
ipv6 unicast-routing
! Static route may need to be altered to match AdminServer's gateway
ip route 0.0.0.0 0.0.0.0 10.200.102.1
ipv6 route ::/0 2001:db8:64:2::1
ip dhcp excluded-address 10.1.10.1 10.1.10.5
ip dhcp pool Students
DNS-server 8.8.8.8
default-router 10.1.10.1
domain-name k12.local
lease 0 4
network 10.1.10.0 255.255.255.128
ipv6 dhcp pool Students6
address prefix 2001:db8:1:8::/64
dns-server 2001:4860:4860::8888
ipv6 default-gateway 2001:db8:1:8::1
domain-name k12.local
ip dhcp excluded-address 10.1.10.129 10.1.10.134
ip dhcp pool Faculty
DNS-server 8.8.8.8
default-router 10.1.10.129
domain-name k12.local
network 10.1.10.128 255.255.255.192
ipv6 dhcp pool Faculty6
address prefix 2001:db8:1:9::/64
dns-server 2001:4860:4860::8888
ipv6 default-gateway 2001:db8:1:9::1
domain-name k12.local
ip dhcp excluded-address 10.1.10.193 10.1.10.198
ip dhcp pool Staff
DNS-server 8.8.8.8
default-router 10.1.10.193
domain-name k12.local
network 10.1.10.192 255.255.255.192
ipv6 dhcp pool Staff6
address prefix 2001:db8:1:A::/64
dns-server 2001:4860:4860::8888
ipv6 default-gateway 2001:db8:1:A::1
domain-name k12.local
ip dhcp excluded-address 10.1.11.1 10.1.11.5
ip dhcp pool ITmgmt 
DNS-server 8.8.8.8
default-router 10.1.11.1
domain-name k12.local
network 10.1.11.0 255.255.255.224
ip dhcp pool WebServers
DNS-server 8.8.8.8
ip default-gateway 10.200.100.1
domain-name k12.local
network 10.200.100.0 255.255.255.0
ipv6 dhcp pool WebServers6 
address prefix 2001:db8:64:0::/64
dns-server 2001:4860:4860::8888
ipv6 default-gateway 2001:db8:64:0::1
domain-name k12.local
ip dhcp pool HRServers 
DNS-server 8.8.8.8
ip default-gateway 10.200.101.1
domain-name k12.local
network 10.200.101.0 255.255.255.0
ipv6 dhcp pool HRServers6 
address prefix 2001:d8:64:1::/64
dns-server 2001:4860:4860::8888
ipv6 default-gateway 2001:db8:64:1::1
domain-name k12.local
ip dhcp pool AdminServers 
DNS-server 8.8.8.8
ip default-gateway 10.200.102.1
domain-name k12.local
network 10.200.102.0 255.255.255.0 
ipv6 dhcp pool AdminServers6
address prefix 2001:db8:64:2::/64
dns-server 2001:4860:4860::8888
ipv6 default-gateway 2001:db8:64:2::1
domain-name k12.local
ip dhcp pool ITmgmt 
DNS-server 8.8.8.8
ip default-gateway 10.200.150.1
domain-name k12.local
network 10.200.150.0 255.255.255.128
int g0/0/0
ipv6 dhcp server automatic
ipv6 add 2001:db8:64:2::a/64
ipv6 add FE80::4
ip add 10.200.102.10 255.255.255.0
no shut

```

</summary> </details>




<details> <summary>DC-ALS</summary>

```
en
config t
hostname DHCP
no ip domain-lookup
line con 0
password cisco
login
logging sync
enable secret class
service password-encryption
ip domain name k12.local
crypto key generate rsa
1024
ip ssh ver 2
username student secret cisco
username admin priv 15 secret cisco
line vty 0 15
transport input ssh
login local
banner motd % keep out %

!------------ vlan stuff -------------------------

int vlan 100
name WebServers
exit
int vlan 101
name HRServers
exit
int vlan 102
name AdminServers
exit
int vlan 150
name ITmgmt
exit
int vlan 900
name BlackHole
int vlan 1000
name NativeOnly


! Does this need vlans 11-13???

!! ADD DHCP RELAY STUFF should be config-if???
ip helper-address 10.200.102.10
ipv6 nd prefix default no-autoconfig
ipv6 dhcp relay destination 2001:db8:64:2::a




!--------- spanning tree stuff------

! apply these three to all switches
    !15a - use the faster version of STP
        spanning-tree mode rapid-pvst 

    !15e - access ports shoud go active immediatly
        spanning-tree portfast default        

    !15f - error disable if receive bpdu
        spanning-tree portfast bpduguard default


! --------   this is security stuff ---------------------
! This applies to all switches
    !20a - learn 3 mac addresses. don't put them in running conf in student vlan
        int vlan 11
        switchport mode access
        switchport port-security maximum 3
        switchport port-security

    !20b - remove mac address after 3 min of inactivity in student vlan
        switchport port-security aging type inactivity
        switchport port-security aging time 3

    !20c - after violations, block bad traffic, send syslog message in student vlan
        switchport port-security violation restrict 
        exit
    !21a - enable dhcp snooping vlan 11-13 or 100-102
        ip dhcp snooping vlan 11
        ip dhcp snooping vlan 12
        ip dhcp snooping vlan 13

    !21b - arp inspection on vlan 11-13 & 100-102, inspect src-mac & ip. 11-13
        ip arp inspection vlaidate src-mac ip
        no ip dhcp snooping information option




```


</summary> </details>




<details> <summary>DC-DLS</summary>


```
en
config t
hostname DHCP
no ip domain-lookup
line con 0
password cisco
login
logging sync
enable secret class
service password-encryption
ip domain name k12.local
crypto key generate rsa
1024
ip ssh ver 2
username student secret cisco
username admin priv 15 secret cisco
line vty 0 15
transport input ssh
login local
banner motd % keep out %


! ---------------- VLAN STUFF ---------------

int vlan 11
name Students
exit
int vlan 12
name Staff
exit
int vlan 13
name Faculty
exit

int range vlan 11-13
ipv6 nd prefix default no-autoconfig
switchport nonegotiate


int range g1/0/21-24
shut
channel-group 1 mode active
int po1
shut
switchport nonegotiate
switchport mode trunk
switchport trunk allowed vlan 11,12,13,50
switchport trunk native vlan 1000
no shut




!! ADD DHCP RELAY STUFF should be config-if???
ip helper-address 10.200.102.10
ipv6 nd prefix default no-autoconfig
ipv6 dhcp relay destination 2001:db8:64:2::a






!--------- spanning tree stuff------

!15d - force dc-dls to be the root for data center vlans





!--------------Routing stuff
! ---- See step 16 b-e





!------- SECURITY STUFF -----------------
int range g1/0/3-24
shut
switchport mode access
switchport access vlan 900
exit




! This applies to all switches
!20a - learn 3 mac addresses. don't put them in running conf in student vlan
    int vlan 11
    switchport mode access
    switchport port-security maximum 3
    switchport port-security

!20b - remove mac address after 3 min of inactivity in student vlan
    switchport port-security aging type inactivity
    switchport port-security aging time 3

!20c - after violations, block bad traffic, send syslog message in student vlan
    switchport port-security violation restrict 
    exit
!21a - enable dhcp snooping vlan 11-13 or 100-102
    ip dhcp snooping vlan 11
    ip dhcp snooping vlan 12
    ip dhcp snooping vlan 13

!21b - arp inspection on vlan 11-13 & 100-102, inspect src-mac & ip. 11-13
    ip arp inspection vlaidate src-mac ip
    no ip dhcp snooping information option


!-------------- WAN 1 and 2 ------------------

int g1/0/1
ip add 10.1.11.33 255.255.255.252
ipv6 add 2001:db8:1:b::/64
int g1/0/2
ip add 10.1.11.37 255.255.255.252
ipv6 add 2001:db8:1:c::/64
int range g1/0/1-2
switchport mode trunk
switchport trunk allowed vlan 11,12,13,50
ip dhcp snooping trust
ip arp inspection trust
no shut

```

</summary> </details>

