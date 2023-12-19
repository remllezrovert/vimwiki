# Networking


[index](index.md)



<details> <summary>Procedural Documents</summary>




[cisco-base-config](cisco-base-config.md) </br>
[cisco-vlsm](cisco-vlsm.md)  </br>
[cisco-vlans](cisco-vlans.md) </br>
[cisco-intervlan-routing](cisco-intervlan-routing.md) </br>
[cisco-static-routing](cisco-static-routing.md) </br>
[Spanning Tree Proceedural](cisco-stp.md) </br>
[cisco-ether](cisco-ether.md) </br>
[cisco-dhcp](cisco-dhcp.md) </br>
[cisco-dhcp6](cisco-dhcp6.md) </br>
[cisco-hsrp](cisco-hsrp.md) </br>
[cisco-security](cisco-security.md)


</summary> </details>


<details> <summary>WLC</summary>

- WLC - Wireless Lan Controller
- A box for wireless stuff

    1. go to ip address of wlan
    2. create the profile and name it similar to the vlan it's on
    3. enable it and select which vlan it should be on
    4. go into the advanced tab and enable 'flexConnect' and 'flexconnect auth'

</summary> </details>





<details> <summary>Security</summary>

[cisco-security](cisco-security.md) </br>
Secure unused ports like this:
```
vlan 1000
name BlackHole
int range g1/0/20-24, g0/0/18-20
shutdown
switchport mode access
switchport access vlan 1000

```

Enable port security on switchport
- only allow one mac address on port
- will shut down port if mac addres number > 1
```
switchport mode access
switchport port-security
end
```

Prevent Vlan hopping attacks
```
!non trunking ports 
switcport mode access
exit

!trunking ports
switchport mode trunk
switchport nonegotiate
switchport trunk native vlan 999
end

!Inactive ports (throw them into blackhole vlan)
switchport mode access
switchport access vlan 1000
exit
```


New Command | What it does
------------|------------
clear port security | removes assigned mac address from secure port
sh port-security int g0/0/1 | display port security information
sh port-security address | show all of the mac addresses and how they were set
(config-if) switchport port-security  | enable switchport security. Must run this 
(config-if) switchport port-security maximum 3 | sets the number of mac addreses on the port. Default is 1
(config-if) switchport port-security mac-address <addressGoesHere> | sets the address
(config-if) switchport port-security mac-address sticky | get mac addresses and save them
(config-if) switchport port-security violation shutdown | if a violation occurs, it is logged, and the device is shut down
(config-if) switchport port-security violation restrict | if a violation occurs, the port drops the packets, device logs the issue
(config-if) switchport port-security violation protect | if a violation occurs, drop the packets. no logging
(config-if) switcport port-security aging type absolue | sets the mac addreses to age constantly.
(config-if) switcport port-security aging type inactivity | sets the mac addresses to only age when inactive.
(config-if) switcport port-security aging static  | do not age addresses.
(config-if) switcport port-security aging time 14 | remove mac address 14 minutes after the aging condition
sh ip dhcp snooping | display snooping information
ip dhcp snooping | globally enable dhcp snooping
ip dhcp snooping vlan 5, 10, 50-60 | enable dhcp snooping on a range of vlans
(config-if) ip dhcp snooping trust | use this for uplinks and server ports. Don't trust user ports
ip dhcp snooping limit rate <packets per second> | use this for end user ports. It mitigates DHCP attacks
(config-if) ip arp inspection trust | don't do arp inspection because interface is trusted
(config-if) ip arp inspection valdiate src-mac | arp inspection mode 
(config-if) ip arp inspection valdiate dst-mac | arp inspection mode
(config-if) ip arp inspection valdiate ip | arp inspecton mode
(config-if) ip arp inspection valdiate src-mac dest-mac ip | Apply multiple modes at the same time
(config-if) no ip dhcp snooping information option | ????????????

To prevent MAC flooding attack
```
int g0/0/0
switcport access vlan 10
switcport mode access 
switchport port-security maximum 5
switchport port-security 
switchport port-security violation restrict
```

To shut down port if there are more than 4 mac addresses
```
int g0/0/0
switcport access vlan 20
switcport mode access 
switchport port-security maximum 4
switchport port-security 
switchport port-security mac-adress sticky
```

Manually configure mac addresses
```
int g0/0/0
switcport access vlan 30
switcport mode access 
switchport port-security 
switchport port-security mac-address aaa.bbb.ccc
```


</summary> </details>




<details> <summary>EtherChannel</summary>

[cisco-ether](cisco-ether.md) </br>


- Combine multiple interfaces to act as one
- Interfaces must have identical speed, duplex, etc
- Interfaces must have idential function (trunk, routed, etc.)

    PAgP modes (Use desirable at all times)
    - 'on' - force this interface to channel without PAgP
    - 'active' - use open source LACP which does the same thing
    - 'PAgP desirable' - nogotiate with others, try to form chanel
    - 'PagP auto' - passive mode, list for channel formation


    ```
    !Configure PAgP mode
    int range g1/0/1-4
    shut
    channel-group 1 mode desireable

    !configure port channel
    int po1 

    !Display the general status of the port channel interface
    sh interfaces port-channel

    !Display one line of information per port channel. Most useful
    sh etherchannel summary

    !Display info about a specific port channel interface
    sh eitherchannel port-channel 

    !Display information about the role of a etherchannel interface
    sh interfaces etherchannel
    ```

</summary> </details>



<details> <summary>static routing</summary>


[cisco-static-routing](cisco-static-routing.md) </br>
[cisco-intervlan-routing](cisco-intervlan-routing.md) </br>
```
int gi0/0
ip add 192.178.1.1 255.255.255.0
duplex auto
speed auto
no shut

```

Types of standard routing:
1. Standard (individual) static route
- `Ip route <unknown network> <mask> <How to get there>`
- **ip route 192.168.3.0 255.255.255.0 192.168.2.2**
2. Default static route
- **ip route 0.0.0.0 0.0.0.0 10.10.10.1**
- routes all traffic to the second router
3. Floating static route
- Usually used as a backup
- Will only appear on the route table if the primary route fails
- The route with the lowest administrative distance is the only one on the route table
- setting distance to 130 is reccomended
```
route rip
version 2
no auto-summary
network 192.168.2.0

```
- Summary static route
General format is:
- `ip route <final destination network address><mask><second router address>`
Floating route format:
- Ip route <receiver network> <mask> <how to get there> <distance>


How to get there:
1. Use "Next-hop route" method if the IP is reachable connected network. ALWAY USE THIS ONE IN CLASS.
- **ip route 192.168.3.0 255.255.255.0 192.168.2.2**
2. Use "directly connected" method if you want to exit a specific interface
- **ip route 192.168.3.0 255.255.255.0 s0/0/0**
3. Use "fully specified" for most possible reliability
- **ip route 192.168.3.0 255.255.255.0 s0/0/0 192.168.2.2**





</summary> </details>


<details> <summary>Spanning tree</summary>

[Spanning Tree Proceedural](cisco-stp.md) </br>
- Redundency can create loops which result in broadcast storms and duplicate unicast frames.
- "Port flapping" getting multiple copies of the same mac address from different ports. PROBLEM
- Spanning tree prevents this by blocking one of the links if a storm is detected
- The 'Root bridge' is the most centerally located switch using in spanning tree STP
- Bridge Protocal Data Unit 'BPDU' contains a 'BID' for determining the root bridge
- A 'BID' or bridge id,  has a mac address, vlan id, and a bridge priority (lower is better)
- PVST:  if there are two possible routes to a device, load balence across both switches
- RSTP:  Load balencing STP, backwards compatable, 

```
!Enables modern PVST mode
spanning-tree mode rapid-pvst

!Sets as root bridge
spanning-tree vlan 1 root primary
end

!backup root bridge
spanning-tree vlan 1 root secondary
end

!set BID priority (lower is better)
spanning-tree vlan 1 priority 24576
end

sh spanning-tree


spanning-tree portfast !disable spanning tree
spanning-tree portfast edge default 
spanning-tree portfast default
spanning-tree portfast bpduguard default !global safeguard to prevent broadcast storm
spanning-tree bpduguard enable !single interface safeguard to prevent broadcast storm
spanning-tree portfast edge bpduguard default
spanning-tree portfast bpduguard default
```



</summary> </details>






<details> <summary>Trunks and vlans</summary>

[cisco-vlans](cisco-vlans.md)


* vLans are basically groups of ports on the same switch that are logically separated into groups.
* ISL - Inter Switch Link trunks.
    + tag all traffic going through the trunk with a vLan ID allowing multiple vLans to use one cable. 
    + trunk is used to connect multiple switches with multiple vLans while keeping traffic separated.
* 802.1q Trunk
    + Native vLans have Un-tagged traffic for security to stop "spoofed tag attacks". 



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



</summary> </details>

<details> <summary>Basic Commands </summary>

#### Command Modes
   prompt       |   Name of mode     | purpose
----------------|--------------------|------------
Router>         | user exec mode     | the first mode used at login, few privs
Router#         | priv exec mode     | do basic things like ping, ssh, and set the system clock
Router(config)# | global config mode | the mode used to edit most settings on routers or switches
Router(config-line)#| line config mode | sub mode within global, used to edit ssh  and console connections 
Router(config-if)#  | interface config | sub mode within gloabl, used to edit interfaces



#### Priv Exec Mode

  command                 |  purpose 
--------------------------|---------
show running-config       | show the configuration running in ram
copy run start            | save the current running configuration as the startup configuration
config t                  | enter global config mode
reload                    | restart the device
clock set 07:13:00 October 15 2022 | purpose is self evident
ping                      | network troubleshooting
tracert                   | network troubleshooting
ssh 92.168.1.100          |  remote access


#### Global Config Mode
  command                 |  purpose 
--------------------------|---------
line vty 0 15 | enter line config mode to edit ssh
line con 0 | enter line config mode 
interface gigabitEthernet 0/0/0 | enter interface config mode
hostname R1 | sets the hostname of the device
banner motd "no unauthorized access is allowed" | sets the motd
enable password class | sets password  'class" for restricting access to priv exec mode
enable secret class | sets encrypted password 'class' for restricting access to priv exec
service password-encryption | sets encryption on all passwords


#### Line Config Mode
  command                 |  purpose 
--------------------------|---------
password cisco | enter the terminal
login | enter for configuration
transport input ssh | allows remote access on this vty

#### Interface Config Mode
  command                 |  purpose 
--------------------------|---------
interface g0/0/0          | configure interface on router 
interface vlan1 | configure interface on switch
ip address 192.168.1.1 255.255.255.0 | configure ipv6 addresses on switches or routers
ipv6 add 2001:db8:224:0::1/64 | configure ipv6 addresses on routers
no shutdown               | turn on the interface



</summary> </details>















