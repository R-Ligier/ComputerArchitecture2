## Computer Architecture 2 - Exam 2 Review

### **Chapter 4.1 - 4.4**
_________________________________________________________________________________________________________________


#### **1.1 Bit Width**

1. Given this sign extend unit, what are the normal bitwidth iof input and output?

    A: The sign extension unit has a 16-bit input and 32-bit output

2. If we change the MIPS word size to 64-bits but the offset width stays the same, how many more bits will be added to the value?

    A:


#### **1.2 - Figure 4.2**

![figure4.2](https://github.com/R-Ligier/ComputerArchitecture2/blob/master/figure4.2.png "Figure 4.2")

- Includes a subset of the hardware needed for the MIPS ISA.
- We’d like to add hardware for a new instruction: LW Rt,Rd(Rs)
- This instruction has the following result: Reg[Rt] = Mem[Reg[Rd] + Reg[Rs]]

1. Which existing logical blocks (if any) can be used for this instruction?

    A:

2. Which new functional blocks do we need for this instruction?

    A:

3. What new signals do we need (if any) for the control to support this instruction?

    A:

#### **1.3 - Figure 4.9**

![figure4.9](https://github.com/R-Ligier/ComputerArchitecture2/blob/master/figure4.9.png "Figure 4.9")

1. What instruction uses the hardware shown in 4.9?

    A: beq

2. What operation does the ALU execute for this instruction?

    A: Evaluates the branch condition

3. Will the RegWrite control line be asserted or deasserted for this instruction?

    A:

4. If we wanted to use this same hardware to calculate the address for an unconditional branch, what value or component could we remove?

    A: Can remove the add component (not sure if this is right)

#### **1.4 - Figure 4.11**

![Figure 4.11](https://github.com/R-Ligier/ComputerArchitecture2/blob/master/figure4.11.png "Figure 4.11")

1. 5th Ed. Ex. 4.4
2. 5th Ed. Ex. 4.5

### **Appendix B**
_________________________________________________________________________________________________________________

- Combinational logic
- Clocking
- Sum of products

#### **2.1 - Chapter B.2 Boolean Truth Tables/Gates**

- **OR operator is written as +, as in A+B**
    - Result is 1 if either of the variables is 1.
    - Called a logical sum, since its result is 1 if either operand is 1.
-  **AND operator is written as  * , as in A*B**
    - Result is 1 only if both inputs are 1.
    - Called logical product, since its result is 1 only if both operands are 1.
- **NOT operator is written as Ā**
    - Result is 1 only if the input is 0.
    - Acts as an inversion or negation of the value (i.e., if the input is 0 the output is 1, and vice versa).

- **Boolean Algebra -  Laws**

![Boolean Laws](https://github.com/R-Ligier/ComputerArchitecture2/blob/master/boolLaws.png " ")

### **2.2 - Chapter B.3 Combinaional Logic**

#### **Decoder**

![Decoder](https://github.com/R-Ligier/ComputerArchitecture2/blob/master/decoder.png "Decoder")

- 3 in 8 out binary decoder
- Three input lines are used to output all the possible values for 3 bits (0 - 7)

#### **Mux (Multiplexor)**

- Multiplexor selects which input to output based on the control/selector value
- If A = 0 , and B = 1 , depending on S , the mux will output either A or B : C = (A ∧ S¯) ∨ (B ∧ S)

#### **Products of Sum | Sum of Products**

- Only two level of gates: AND, OR
    - Sum of products = Logical sum (OR) of products (terms using AND operator)
    - Products of sum = Logical sum (AND) of products (terms using OR operator)


#### **2.3 - Chapter B.8 Setup and Hold Time**

- Timing is everything for sequential circuits.
- Setup - the data line is set ten the clock signals.
- After some time held , the data value of Q will change, this actually sets our D-flipflop to a new
state.

1. Why do we need to setup and hold time for writing values?

    A:

2. If the data values change, but the clock never changes, is it possible to set a new value in Q?

    A:

#### **2.4 - Chapter B.8 Register File**

- One of the main parts of the data path (CPU) is the REGISTER FILE
- This is basically a set of registers that can be read or written.
- We can implement the registers themselves from D-flipflops.
- By adding a decoder for the read and write ports, we can use the register file to hold the instructions we’ve been talking about for assembler code.

1. We can have 2 read ports and 1 write port. Why?

    A:
    
2. What does reading do to the state of the register?

    A:
    
3. What about writing?

    A:
    
4. Can we read and write to the same register on the same clock cycle?

    A:

### **Multicycle**
_________________________________________________________________________________________________________________

![Multi-Full](https://github.com/R-Ligier/ComputerArchitecture2/blob/master/multi-full.png "Multi-Full")

1. How many control lines are required for the ALUSrcB multiplexor?

    A:

2. What number and 2 bit value are used on the ALUSrcB multiplexor to increment the PC?

    A:

3. What are the 2 data sources for the MUX controlled by the MemtoReg control line?

    A:

#### **Finite State Machine**

![fsm-fetch](https://github.com/R-Ligier/ComputerArchitecture2/blob/master/fsm-fetch.png "fsm-fetch")

1. According to the figure, what is the value of ALUOp, for these 2 states?

    A:

2. According to fig.FSM-FETCH and fig.MULTI-FULL, what input will be selected during state 1 for ALUSrcB?

    A:

3. For Q2 above, what instruction is associated with this input to ALUSrcB?

    A:

