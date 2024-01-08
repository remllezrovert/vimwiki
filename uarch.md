
# $\mu arch$
[index](index.md) </br>
[assembly](assembly.md) </br>




<details> <summary>Instructions</summary>

- Each item in the 'name' column has an opcode

Name | desc | addresses/registers
-----|------|---------------
mov | read RAM location into register X | RAM address
push | write from a register X into a RAM location | RAM address
ADD | add two registers, store the value in the second | two register ID's



</summary> </details>



<details> <summary>ALU</summary>

Inputs
- two registers
- opcode

Outputs
- flags (positive/negative)
- result


</summary> </details>


<details> <summary>Control Unit</summary>


Parts:
- Clock
- instruction register (stores the instruction plucked from memory)
- Address register (stores the memory address where the instruction was found)

What it does:
- Reads from memory addresses in order
- skip to memory address if 'jump' instruction is received

To add/subtract/multiply two numbers, both numbres need to be loaded into registers
</summary> </details>


<details> <summary>RAM</summary>

Populated ram addreses store data with two parts
1. The opcode specifies which instruction/operation the ALU should execute
2. Data that specifies which CPU register or RAM address to perform the instruction on


</summary> </details>







