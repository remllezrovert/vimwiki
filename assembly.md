# RISC-V Assembley
[uarch](uarch.md) </br>
[index](index.md) </br>


ISA - Instruction set archetecture

<details> <summary>Basics </summary>

Structure: </br>
<operation> <dst>,<src1>,<src2> </br>

example:
```asm
addi a2, x0, 64                  # Add 64 to 0, place the result into register a2
la a1, hello                     # Load the address (labeled hello) into register a1
```




```asm
.global _start
.section .text
_start:
	li a0, 1                      # Load immediate 1, this means linux stdout
	la a1, hello                  # Load the address (labeled hello) into register a1
	li a2, 13                     # Set the size of the ascii string to 13 characters (count starts at 1)
	li a7, 64                     # Write to output
	ecall                         # This executes the lines above

    li a0, 0                      # Load immediate 0, this means linux stdin
    li a7, 93                     # This (93 in a7) causes the program to exit 
    ecall                         # This excutes the lines above

.section .data                    # Variables live in the data section
hello: .ascii "Hello World\n"     # This memory address labeled 'hello' stores an ascii string
```

</summary> </details>


<details> <summary>32 bit</summary>

32 bits registers cannot be loaded all at once. </br>
They must be loaded in two parts. The upper and </br>
lower parts. 

```asm
.data
num:
    .word 5
nmPtr:
    .word 0

    .text
main:
    lui t0, %hi (num)A         # Load the upper 20 bits to t0
    addi t0, t0, %lo (num)     # Add the bottom 12 bits to t0

```


</summary> </details>






<details> <summary>Conventions and macros</summary>




calling convention| what it does | desc
------------------|--------------|----
syscall | perform action using OS | 
ecall | trigger interrupt |
sw | store word | store word in register at memory address
lw | Load Word | load word from memory into register
la | load address  (memory) | load memory address into register
li | load immediate | load integer directly into a register
lui | load upper immediate (see 32 bit info)
jal | Jump and Link
jalr | Jump and Link Return
add \$t1, \$t3, \$t4 | addition | add \$t3 and \$t4
addi | add immediate | add integer(s) directly into register
bne \$t1, \$t2, L1 | branch not equal 
beq \$t1, \$t2, L1 | branch on equal
ble \$t1, \$t2, L1 | branch on less/equal
bge \$t1, \$t2, L1 | branch greater/equal
slt \$t3, \$t2, \$t1 | set register (bool) on less than | places 1 or 0 into \$t3



macros | desc
-------|------
%hi | access first bits of register
%lo | access last bits of register

</summary> </details>




<details> <summary>Registers</summary>

- See "System calls" for more info about those registers

ABI Name | quantity | desc
---------|----------| ----
t0-t6 | 7 | temporary: calling separate function will wipe register
s0-s11 | 12 | saved registers: non-volitile, data will persist until function returns
a0-a7 | 8| argument: How you pass args into functions



Register | ABI Name | Desc | Saver
---------|----------|------|------
x0 | zero | hard-wired zero | n/a
x1 | ra | return-address | caller
x2 | sp | stack pointer | callee
x3 | gp | global pointer | n/a
x4 | tp | thread pointer | n/a
x5 | t0 | temp/alt link register | caller
x6-7 | t1-2 | Temps | caller
x28-31 | t3-6 | Temps |  caller
x8 | s0/fp | Saved register/Frame pointer | callee
x9 | s1 | saved register | callee
x18-27 | s2-11 | saver registers | callee
x10-11 | a0-1 | function arguments / return values  | caller
x12-17 | a2-7 | Function arguments | caller





</summary> </details>



<details> <summary>System Calls</summary>



- Use register a7 for system calls
- Place the arguments for the system call in a0

[Syscall Table](https://syscalls.w3challs.com/?arch=mips_o32)

name | #  | Params
-----|----|----
exit | 93 | N/A
write | 64 | address label, string length



</summary> </details>



<details> <summary>Memory</summary>

- Byte addressable array
- Words stored in little-edian byte order (RISC-V)
- Stores code and data
- Stack for procedure calls

</summary> </details>








