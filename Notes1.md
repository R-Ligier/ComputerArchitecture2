### **The Compiler - Translation Hierarchy**
Code -> Compiler -> Assembly Language Program -> Assembler -> 2 Binary Object Files -> Linker -> Executable -> Loader -> Memory

The code is compiled into an assembly language program and then assembled into two binary object files. The linker combines multiple modules with library routines to resolve all refrences. The loader then places the machine code into the proper memory locations for execution by the processor.

### **Basic MIPS Implementation**
- Memory instructions = load word (lw), store word (sw)
- Arithmetic-logical instructions = add, SUB, AND, OR, slt (shift left logical)
- Branches = branch equal (beq) and jump (j)

#### **Overview of implementation**
For every instruction the two setps are identical:

1. Send the program counter (PC) to the memory that contains the code and fetch the instruction from that memory.
2. Read 1-2 registers, ujsing fields of the instruction to select the registers to read. For the **load instruction**, need to read only one register. Most other instructions require more than one register.

After the two steps, next steps taken are dependent on the instruction class. However, for all instruction classes excluding jump, use the ALU for address calculations, arithmetic operations, and comparisons for branches:

1. Memory Instruction - will need to access the memory either to read data for a load or write data for a store.
2. Arithmetic-Logical or Load Instruction - must write the data from the ALU or memory back into a register.
3. Brand Instructions - may need to change the next instruction branch based on the comparison; oherwise, the PC should be incrementeed by 4 to get the next instruction.

#### **An abstract view of the implementation of the MIPS subset showing the major functional units and the major connections between them.**

![figure4.1](https://github.com/R-Ligier/ComputerArchitecture2/blob/master/figure4.1.png "Figure 4.1")

All instructions start by using the program counter to supply the instruction address to the instruction memory. After the instruction is fetched, the register operands used by an instruction are specified by fields of that instruction. Once the register operands have been fetched, they can be operated on to compute a memory address (for a load or store), to compute an arithmetic result (for an integer arithmetic-logical instruction), or a compare (for a branch).
If the instruction is an:
- **Arithmetic-logical instruction:** result from the ALU must be written to a register.
- **Operation is a load or store:** the ALU result is used as an address to either store a value from the registers or load a value from memory into the registers. The result from the ALU or memory is written back into the register file.
- **Branches:** require the use of the ALU output to determine the next instruction address, which comes either from the ALU (where the PC and branch offsets are summed) or from an adder that increments the current PC by 4.

#### **The basic implementation of the MIPS subset, including the necessary multiplexors and control lines**
//put figure 4.2 here

### **Building a Datapath**
Datapath elements each instruction needs:

1. Memory unit - store the instructions of a program and supply instructions given an address.
2. Program counter - register that holds the address of the current instruction.
3. Adder - increment the PC to the address of next instruction.

//put figure 4.6

**R-Format/Type Instructions (arthmetic-logical) = Performs arithmetic/logical operations:**
- R-format has three register operands:
- Example: add $t1, $t2, $t3 - $t2 and t3 reads and $t1 writes
1. Will need a register file and ALU

//put figure 4.7

**Load/Store Word Instructions:**
- General form = lw $t1, offet_value($t2), sw $t1, offset_value ($t2)
- Computes a memory address by adding the base register ($t2) to the 16-bit signed offset field contained in the instruction.
- If instruction is a store = value to be stored must also be read from the register file where it resides in $t1.
- If instruction is a load = the value read from memory must be written into the register file in the specified register ($t1).
- Need both the register file and the ALU.
- Need to sign-extend the 16-bit offset field in the instruction to a 32-bit signed value and a data memory unit to read from or write to.

**Branch Equal (beq) Instruction:**
- General form = beq $t1, $t2, offset
- Has 3 operands = 2 registers used to compare for equality and a 16-bit offset used to compute the branch target address.
- To implement beq:
- Uses the ALU to evaluate the branch condition
- Separate adder to compute the branch target as the sum of the incremented PC and the sign-extended, lower 16-bits of the instruction, shifted left 2 bits.

//put figure 4.9

### **Creating a Single Datapath**
- Put all datapath components in one to create a single datapath and add the control to complete the implementation
- Simplest datapath is to execute all instructions in one clock cycle
- Means no datapath resource can be used more than once per instruction
- If element needed more than once, it must be duplicated.
- Need a memory for instructions separate from one for data
-

### **Pipelining**
Implementation technique in which multiple instructions are overlapped in execution.


### **Terminology**
- **Arithmetic Logic Unit (ALU):** Hardware that performs the arithmetic operations and usually logical operations such as AND and OR.
- **Datapath Element:** Unit used to operate on or hold data within a processor. In MIPS, the datapath elements include the instruction and data memories, the register file, the ALU, and the adders.
- **Register File:** Collection of registers in which any register can be read or written by specifying the number of the register in the file. It also contains the register state of the computer.
- **Program Counter (PC):** The register containing the address of the instruction in the program being executed.
- **Decoder:** Has n-bit input and 2n-bit outputs and only one of the outputs is asserted for each input combination.
- Example: 3 bits inputted, 2 x 3 bits outputted.
- **Multiplexors:** Can be thought of as a "selector" since its output is one of the inputs that is selected by a control unit.'
- **Control Unit:** Instruction as an input and used to determine how to set the control lines for the functional units and multiplexors.
- **Asserted:** The signal is logically high or true.
- **Deasserted:** The signal is logically low or false.
- **Sign Extended:** To increase the size of a data item by replicating the high-order sign bit of the original data item in the high-order bits of the larger, destination data item.
- **Branch Target Address:** Address specified in a branch, which become the new PC if the branch is taken. Branch target is given by the sum of the offset field of the instruction and the address of the instruction following the branch.

