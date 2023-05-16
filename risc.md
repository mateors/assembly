# The ARM is what is called a RISC computer
> RISC stands for Reduced Instruction Set Computer

> RISC is a type of microprocessor architecture that utilizes a small, highly-optimized set of instructions, rather than a more specialized set of instructions often found in other types of architectures. The goal of RISC architecture is to reduce execution time by simplifying the instruction set of the computer.

## CPU Registers
The registers are part of the CPU circuitry allowing instant access, whereas memory is a separate component and there is a transfer time for the CPU to access it.

> The ARM processor is based on a **load-store architecture** where there are two basic types of instructions:

1. Instructions that either load memory into registers or instructions that store data from registers into memory
2. Instructions that perform arithmetical or logical operations between two registers

If you want to add two numbers, you might do the following:
1. Load one into one register and the other into another register.
2. Perform the add operation putting the result into a third register.
3. Copy the answer from the results register into memory.
As you can see, it takes quite a few instructions to perform simple operations.

## Registers in ARM Processor
1. General-purpose registers - 31 (X0–X30)
2. a program counter (PC) - 1 
3. a combination zero register/stack pointer - 1
4. Link Register - X30, LR 

## X30, LR 
If you call a function, this register will be used to hold the return address. As this is a common operation, you should avoid using this register for other things.
## SP, XZR
The stack pointer or zero register depending on the context.

We don’t always need the full 64 bits of data in a register. Often 32 bits is fine. All the X registers can be operated on as 32-bit registers by referring to them as `W0–W30` and `WZR`. When we do this, the instruction will use the lower 32 bits of the register and set the upper 32 bits to zero. Using 32 bits saves memory, since you only use 4 bytes rather than 8 bytes for each quantity saved. Most loop counters and other common variables used in programming easily fit in 4 bytes, so this is made easy by the processor.

> There are a large set of registers for the coprocessors:
* Floating-Point Operations.
* Neon Coprocessor.

