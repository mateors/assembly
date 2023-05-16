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

## 32 Registers in ARM Processor
1. General-purpose registers - 31 (`X0–X30`)
2. a program counter (PC) - 1  (The memory address of the currently executing instruction.)
3. a combination zero register/`stack pointer` SP|XZR -1 (special purpose)
4. Link Register - X30, LR 

## X30, LR -> Link register
If you call a function, this register will be used to hold the return address. As this is a common operation, you should avoid using this register for other things.

## SP, XZR
The stack pointer or zero register depending on the context.

We don’t always need the full 64 bits of data in a register. Often 32 bits is fine. All the X registers can be operated on as 32-bit registers by referring to them as `W0–W30` and `WZR`. When we do this, the instruction will use the lower 32 bits of the register and set the upper 32 bits to zero. Using 32 bits saves memory, since you only use 4 bytes rather than 8 bytes for each quantity saved. Most loop counters and other common variables used in programming easily fit in 4 bytes, so this is made easy by the processor.

> There are a large set of registers for the coprocessors:
* Floating-Point Operations.
* Neon Coprocessor.

## ARM Instruction Format
Each ARM binary instruction is 32 bits long. Fitting all the information for an instruction into 32 bits is quite an accomplishment requiring using every
bit to tell the processor what to do. There are quite a few instruction formats, and it can be helpful to know how the bits for each instruction are packed into 32 bits. Since there are 32 registers (the 31 general-purpose registers plus the stack pointer (SP)/zero register (XZR)), it takes 5 bits to specify a register. Thus, if you need three registers, then 15 bits is taken up
specifying these.

> Having small fixed length instructions allows the ARM processor to load multiple instructions quickly. It doesn’t need to start decoding an instruction to know how long it is and hence where the next instruction starts. This is a key feature to allowing processing parallelism and efficiency.

> Each instruction that takes registers can either use the 32-bit W version or the 64-bit Z version. To specify which is the case, the high bit of each instruction specifies how we are viewing the registers

```All the registers in a single instruction need to be the same—you can’t mix W and Z registers```

* Bits: If this bit is zero, then any registers are interpreted as the `32-bit W` version. If this bit is one, then they are the full `64-bit X` version of the register.
* Opcode: Which instruction are we performing, like ADD or MUL.
* Shift: These two bits specify shifting operations that could be applied to the data.
* Set condition code: This is a single bit indicating if this instruction should update any condition flags. If we don’t want the result of this instruction to affect following branch instructions, we would set it to 0.
* Rm, Rn: Operand registers to use as input.
* Rd (destination register): Where to put the result of whatever this instruction does.
* Imm6: An immediate operand which is usually a small bit of data that you can specify directly in the instruction. So, if you want to add 1 to a register, you could have this as 1, rather than putting 1 in another register and adding the two registers. These are usually the bits left over after everything else is specified.


> When things are running well, each instruction executes in one clock cycle. 

An instruction in isolation takes three clock cycles: 
1. one to load the instruction from memory, 
2. one to decode the instruction, and then
3. one to execute the instruction. 

The ARM is smart and works on three instructions at a time, each at a different step in the process, called the instruction pipeline. If you have a linear block of instructions, they all execute on average taking one clock cycle.

> In modern ARM processors, the execution pipeline is much more sophisticated and can be working on more than three instructions at a time.
>  out-of-order execution
