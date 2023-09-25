# Networking
[index](index.md)
[java](java.md)
[database](database.md)


##### [cisco-vlsm](cisco-vlsm.md)  </br>


##### [cisco-base-config](cisco-base-config.md) </br>

[cisco-vlans](cisco-vlans.md)







<details> <summary>Trunks and vlans</summary>

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

<details> <summary>Commands </summary>

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










[index](index.md)





