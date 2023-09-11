# Networking
[index](index.md)
[java](java.md)
[database](database.md)

<details> <summary>VLSM</summary>

Refer to [cisco-vlsm](cisco-vlsm.md) for detailed instructions

</summary> </details>


<details> <summary>Command modes</summary>


   prompt       |   Name of mode     | purpose
----------------|--------------------|------------
Router>         | user exec mode     | 
Router#         | priv exec mode     |
Router(config)# | global config mode | 


sub modes of global config mode
prompt              | name             |  purpose
--------------------|------------------|-----------
Router(config-line)#| line config mode | edit ssh  and console connections 
Router(config-if)#  | interface config | edit interfaces

</summary> </details>



<details> <summary>Priv exec mode</summary>

  command                 |  purpose 
--------------------------|---------
show running-config       | show the configuration running in ram
copy run start            | save the current running configuration as the startup configuration
config t                  | enter global config mode
reload                    | restart the device
clock set 07:13:00 October 15 2022 | 
ping                      |
tracert                   |
ssh 92.168.1.100          | 

</summary> </details>

<details> <summary>Global config mode</summary>


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


</summary> </details>



<details> <summary>line config mode</summary>


  command                 |  purpose 
--------------------------|---------
password cisco | enter the terminal
login | enter for configuration
transport input ssh | allows remote access on this vty


</summary> </details>


<details> <summary>interface config mode </summary>


  command                 |  purpose 
--------------------------|---------
interface g0/0/0          | 
ip address 192.168.1.1 255.255.255.0 |
no shutdown               | turn on the interface


</summary> </details>

[index](index.md)





