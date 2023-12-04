




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
! commands below this point are unqiue to routers
line aux 0
password cisco
login
ipv6 unicast-routing
! Static route may need to be altered to match AdminServer's gateway
ip route 0.0.0.0 0.0.0.0 10.200.102.1
ipv6 route ::/0 2001:db8:64:2::1
ip dhcp pool Students
DNS-server 8.8.8.8
default-router 10.1.10.1
domain-name k12.local
lease 0 4
ip dhcp excluded-address 10.1.10.1 10.1.10.5
network 10.1.10.0 255.255.255.128
ipv6 dhcp pool Students6
address prefix 2001:db8:1:8::/64
dns-server 2001:4860:4860::8888
default-gateway 2001:db8:1:8::1
domain-name k12.local
ip dhcp pool Faculty
DNS-server 8.8.8.8
default-router 10.1.10.129
domain-name k12.local
ip dhcp excluded-address 10.1.10.129 10.1.10.134
network 10.1.10.128 255.255.255.192
ipv6 dhcp pool Faculty6
address prefix 2001:db8:1:9::/64
dns-server 2001:4860:4860::8888
default-gateway 2001:db8:1:9::1
domain-name k12.local
ip dhcp pool Staff
DNS-server 8.8.8.8
default-router 10.1.10.193
domain-name k12.local
ip dhcp excluded-address 10.1.10.193 10.1.10.198
network 10.1.10.192 255.255.255.192
ipv6 dhcp pool Staff6
address prefix 2001:db8:1:A::/64
dns-server 2001:4860:4860::8888
default-gateway 2001:db8:1:A::1
domain-name k12.local
ip dhcp pool ITmgmt 
DNS-server 8.8.8.8
default-router 10.1.11.1
domain-name k12.local
ip dhcp excluded-address 10.1.11.1 10.1.11.5
network 10.1.11.0 255.255.255.224
ip dhcp pool WebServers
DNS-server 8.8.8.8
default-gateway 10.200.100.1
domain-name k12.local
network 10.200.100.0 255.255.255.0
ipv6 dhcp pool WebServers6 
address prefix 2001:db8:64:0::/64
dns-server 2001:4860:4860::8888
default-gateway 2001:db8:64:0::1
domain-name k12.local
ip dhcp pool HRServers 
DNS-server 8.8.8.8
default-gateway 10.200.101.1
domain-name k12.local
network 10.200.101.0 255.255.255.0
ipv6 dhcp pool HRServers6 
address prefix 2001:d8:64:1::/64
dns-server 2001:4860:4860::8888
default-gateway 2001:db8:64:1::1
domain-name k12.local
ip dhcp pool AdminServers 
DNS-server 8.8.8.8
default-gateway 10.200.102.1
domain-name k12.local
network 10.200.102.0 255.255.255.0 
ipv6 dhcp pool AdminServers6
address prefix 2001:db8:64:2::/64
dns-server 2001:4860:4860::8888
default-gateway 2001:db8:64:2::1
domain-name k12.local
ip dhcp pool ITmgmt 
DNS-server 8.8.8.8
default-gateway 10.200.150.1
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




! -------- Other security -----------------



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
switchport nonegotiate
ipv6 dhcp server Students6
ipv6 nd prefix default no-autoconfig
exit
int vlan 12
name Staff
switchport nonegotiate
ipv6 dhcp server Faculty6
ipv6 nd prefix default no-autoconfig
exit
int vlan 13
name Faculty
switchport nonegotiate
ipv6 dhcp server Staff6
ipv6 nd prefix default no-autoconfig
exit

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





!! ADD DHCP RELAY STUFF



!------- SECURITY STUFF -----------------
int range g1/0/3-24
shut
switchport mode access
switchport access vlan 900
exit
spanning-tree portfast default
spanning-tree mode rapid-pvst
spanning-tree portfast bpduguard default

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

