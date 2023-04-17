# PCASM-BOOK
> http://pacman128.github.io/static/pcasm-book.pdf

> In general, every type of CPU has its own unique machine language.

> This is one reason why programs written for a Mac can not run on an IBM-type PC.


## 8088,8086:
16-bit registers: AX, BX, CX, DX, SI, DI, BP, SP, CS, DS, SS, ES, IP,FLAGS

They only support up to one megabyte of memory and only operate in real mode.

In this mode, a program may access any memory address, even the memory of other programs! This makes debugging and security very difficult! Also, program memory has to be divided into segments. Each segment can not be larger than 64K.


## 80386:
This CPU greatly enhanced the 80286. First, it extends many of the registers to hold 32-bits (EAX, EBX, ECX, EDX, ESI, EDI, EBP, ESP, EIP) and adds two new 16-bit registers FS and GS. It also adds a new 32-bit protected mode. In this mode, it can access up to 4 gigabytes. 

The general purpose registers are used in many of the data movement and arithmetic instructions.


## index registers:
SI and DI

## Pointer registers:
BP and SP

## segment registers:
CS, DS, SS and ES
They denote what memory is used for different parts of a program.
ES is used as a temporary segment register.

## Instruction Pointer (IP) register:
IP register is used with the CS register to keep track of the address of the next instruction to be executed by the CPU. Normally, as an instruction is executed, IP is advanced to point to the next instruction in memory

## FLAGS register:
The FLAGS register stores important information about the results of a previous instruction. These results are stored as individual bits in the
register.

> how individual instructions affect the FLAGS register.




## Real Mode:
In real mode, memory is limited to only one megabyte (220 So where did the infa- bytes). Valid address range from (in hex) 00000 to FFFFF. These addresses require a 20-bit number. Obviously, a 20-bit number will not fit into any of the 8086’s 16-bit registers. Intel solved this problem, by using two 16-bit values to determine an address. 

The first 16-bit value is called the selector. Selector values must be stored in segment registers. The second 16-bit value is called
the offset. The physical address referenced by a 32-bit selector:offset pair is computed by the formula 

> 16 ∗ selector + offset

In real mode, a selector value is a paragraph number of physical memory.

In protected mode, a selector value is an index into a descriptor table. In both modes, programs are divided into segments. In real mode, these segments are at fixed positions in physical memory and the selector value denotes the paragraph number of the beginning of the segment. In protected mode, the segments are not
at fixed positions in physical memory. In fact, they do not have to be in memory at all!

Protected mode uses a technique called virtual memory .


In 16-bit protected mode, segments are moved between memory and disk as needed

In protected mode, each segment is assigned an entry in a descriptor table.

This entry has all the information that the system needs to know
about the segment. This information includes: is it currently in memory;
if in memory, where is it; access permissions (e.g., read-only). The index
of the entry of the segment is the selector value that is stored in segment
registers.

## 32-bit Protected Mode::

 ## pages:
Segments can be divided into smaller 4K-sized units called pages


## Interrupts

