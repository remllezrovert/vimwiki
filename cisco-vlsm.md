

# VLSM Subnetting
By Trevor Zellmer. </br>

Links: </br>
> [cisco](cisco.md) </br>




### Purpose
The purpose of VLSM is to divide computer networks into multiple subnets efficently.
Having multiple subnets can be useful for security reasons. Different subnets can
have different access control lists to regulate incoming and outgoing traffic.



#### Host portion size
An IP address has two portions. The left portion is called the network portion.
The right portion is called the host portion. 
Ip addresses are shown in decmial but they are actually bianary addresses made up of 32 bits.
Ip addresses are divided into four octets, each containing eight bits.
The number of hosts in each subnet can vary wildly, it's best to size each subnet proportionally to it's host population.
</br>



In the subnet 192.168.0.0/24 the /24 indicates the network portion $N_b$ which uses 24 out of 32 bits. </br>
All eight of the remaining bits are in the host portion $H_b$.
The number of bits in the host portion is:
> $H_b$ = 32 - $N_b$ </br>
> $8 = 32 - 24$ </br>

The number of available hosts $H_n$ provided by those bits is found using this sequence: </br>
> (0,2,6,14,30,...) $H_n = 2^{H_b} -2$ </br> </br>

Notice that two is being subtracted away from the value, this is because there are 
two IP addresses that are reserved in every subnet: The broadcast address and the network address. The network address has all zeros in the host portion, resulting in 192.168.0.0.
The broadcast address has all ones in the binary host portion resulting in 192.168.255.255. </br>


___

### Subnetting Proceedure

<table>
<tr><th> Example Problem </th></tr>
<tr><td>

Address | Network portion | Host portion | Available Host Number | Desired number of hosts
--------|-----------------|--------------|-----------------|----------------
192.168.1.0 | /24 | 8 | 252 | 240
192.168.2.0 | /25 | 7 | 126 | 120
192.168.2.128 | /26 | 6 | 62 | 60
192.168.2.192 | /27 | 5 | 30 | 30
192.168.2.224 | /27 | 5 | 30 | 15
192.168.3.0 | /28 | 4 | 14 | 8

</td></tr>
</table>

##### 1. Getting Organized

* a. Draw the column labels of the example table above on the top right corner of a notebook page to organize information. We will call the new table you have created "your table".
* b. Draw a crude diagram of your network on the bottom left corner of a notebook page. Label each subnet with the number of hosts that it will contain

##### 2. Writing out the first row in your table
* a. Write the given starting address in first row address column </br>
* b. Select the largest subnet and write the desired number of hosts in the first row of your table in it's designated column </br>
* c. write the row's corisponding network portion, host portion, and available number based on the desired number of hosts.
    + See the [Host Portion Size](#host-portion-size) guidelines found above for more information. </br>

##### 3. Finding the next address in your table

</br>

<table>
<tr><th> Octet Three </th><th>Octet Four</th></tr>
<tr><td>

$N_b$|/17|/18|/19|/20|/21|/22|/23|/24
---------------|---|---|---|---|---|---|---|---
$H_b$| 15 | 14 | 13 | 12 | 11 | 10 | 9 |8 | 7
$v$|128|64|32|16|8|4|2|1


</td><td>

/25|/26|/27|/28|/29|/30|/31|/32
-|-|-|-|-|-|-|-
7|6|5|4|3|2|1|0
128|64|32|16|8|4|2|1|

</td></tr> </table>


* a.  Find the next largest subnet, and write it's desired number of hosts in the next row
* b. Input the network portion, host portion, and available number based on the desired number of hosts.
    + See the [Host Portion Size](#host-portion-size) guidelines found above for more information. </br>
* c. Use the host bits $H_b$ of the previous address to find the value $v$ using the octet table above.
    + Take note of which octet $v$ is found in we will call this $O$
    + The values in the table are founding using this equation: $v = 2^{mod(H_b,8)}$.

* d. Add $v$ to the $O$ octet of the address in your previous row 
    + If the result is less than 255 then write this address into the ip column of your current row.
     + If the result is greater than or equal to 255 then this value is invalid and a bit shift is needed.
    + Repeat step three until a bit shift is needed. 

##### 4. Bit Shift
* a. Take the address in the previous row of your table and observe the first octet left of $O$
* b. Add one to this octet, and fill the proceeding octets in with zeros.
* c. Write the result into the address row of the current column.
* d. Repeat step three until step four is needed again.




<details> <summary>Math</summary>

$$
\begin{bmatrix}
192 & 168 & 1 & 0 \\
192 & 168 & 2 & 0 \\
192 & 168 & 2 & 128 \\
192 & 168 & 2 & 192 \\
192 & 168 & 2 & 224 \\
192 & 168 & 3 & 0 
\end{bmatrix}
$$



$$A_O = (A-1)_{O} + 2^{mod(H_b,8)}$$
If $A_O \ge 256$ Then: 
$$A_{O-1} = (A-1)_{O-1} + 1$$ </br>

</summary> </details>



##### 5. Vertification and troubleshooting
* a. Double check your math
* b. Visit [a subnetting calculator website](https://subnettingpractice.com/vlsm.html) to vertify that all of your math is correct
* c. Ask someone who knows what they're doing (Tyler Perhaps).

