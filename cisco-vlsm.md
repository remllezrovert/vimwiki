

# VLSM Subnetting

By Trevor Zellmer.


### Purpose
The purpose of VLSM is to divide computer networks into multiple subnets efficently.
Having multiple subnets can be useful for security reasons. Different subnets can
have different access control lists for users with different privileges.



### Basics
A IP address has two portions. The left portion is called the network portion.
The right portion is called the host portion. 
Ip addresses are shown in decmial but they are actually bianary addresses made up of 32 bits.
Ip addresses are divided into four octets, each containing eight bits.
The number of hosts in each subnet can vary wildly, it's best to size each subnet proportionally to it's host population.


<table>
<tr><th> Octet One </th><th>Octet Two</th></tr>
<tr><td>

1|2|3|4|5|6|7|8
-|-|-|-|-|-|-|-
128|64|32|16|8|4|2|1|

</td><td>

9|10|11|12|13|14|15|16
-|-|-|-|-|-|-|-
128|64|32|16|8|4|2|1

</td></tr> </table>

<table>
<tr><th> Octet Three </th><th>Octet Four</th></tr>
<tr><td>

17|18|19|20|21|22|23|24
-|-|-|-|-|-|-|-
128|64|32|16|8|4|2|1


</td><td>

25|26|27|28|29|30|31|32
-|-|-|-|-|-|-|-
128|64|32|16|8|4|2|1|

</td></tr> </table>

### Host portion size


In the subnet 192.168.0.0/24 the /24 indicates the network portion which uses 24 out of 32 bits. </br>
All eight of the remaining bits are in the host portion.
The number of bits in the host portion is:
> $n$ = 32 - 24 = 8  </br></br>

The number of available hosts $H_n$ provided by those bits is found using this sequence: </br>
> (0,2,6,14,30,...) $H_n = 2^n -2$ </br> </br>

Notice that two is being subtracted away from the value, this is because there are 
two IP addresses that are reserved in every subnet: The broadcast address and the network address. The network address has all zeros in the host portion, resulting in 192.168.0.0.
The broadcast address has all ones in the binary host portion resulting in 192.168.255.255. </br>


___

### Subnetting Proceedure

1. Draw a crude diagram of the network on the bottom left corner of a notebook page. Label each subnet with the number of hosts that it will contain

2. Find the most populous subnet, and choose how many bits the host and network portions of the address must be based on the host count. [See host portion size](#host-portion-size) for more information. 

3. Write the number of bits in the network portion on the upper right corner of the notebook page. Draw a slash to the left of this number.


4. Write the first address given to the left of the number 
5. Find the second most populus subnet and write it's host address below the previous host addres
