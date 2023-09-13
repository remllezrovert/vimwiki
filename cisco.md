# Networking
[index](index.md)
[java](java.md)
[database](database.md)


##### [cisco-vlsm](cisco-vlsm.md)  </br>


##### [cisco-base-config](cisco-base-config.md) </br>






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





