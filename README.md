Task 1

Installing the RISC-V Toolchain and Compiling C Code
Step 1: Installing the RISC-V Toolchain via VDI
1.	Check Storage Space
o	Ensure at least 100GB of free space on C or D drive.
2.	Download the VDI File
o	Get the RISC-V VDI file from the link 
o	Unzip the downloaded file.
3.	Set Up VirtualBox (Windows)
o	Windows: Install Oracle VirtualBox (Download).
________________________________________
Step 2: Writing and Compiling C Code on Native GCC
1.	Open Terminal and Navigate to the Desired Directory
   cd /path/to/directory
2.	Create a New C File
   gedit sum_1_to_n.c
o	Write a C program to compute the sum of the first n numbers.
o	Save the file (Ctrl + S) and close (Ctrl + W).
3.	Compile and Execute Using GCC
	gcc sum_1_to_n.c
	./a.out
________________________________________
Step 3: Compiling C Code on RISC-V GCC
1.	Display the C Code in Terminal
	cat sum_1_to_n.c
2.	Compile Using the RISC-V GCC Compiler
	riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum_1_t_on.o sum_1_to_n.c
o	-mabi=lp64: 64-bit integer, long, and pointer size.
o	-march=rv64i: Targets RISC-V 64-bit integer architecture.
o	-O1: Basic compiler optimization.
3.	View the Assembly Code
	riscv64-unknown-elf-objdump -d sum_1_to_n.o
4. To search for only the main assebly code
 riscv64-unknown-elf-objdump -d sum_1_to_n.o | less
o	Use /main to locate the main function in assembly.
5. Compile Using the RISC-V GCC Compiler
	riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sum_1_t_on.o sum_1_to_n.c
6.	View the Assembly Code
	riscv64-unknown-elf-objdump -d sum_1_to_n.o
7. To search for only the main assebly code
 riscv64-unknown-elf-objdump -d sum_1_to_n.o | less
o	Use /main to locate the main function in assembly.

When we use Ofast optimization level, we can see that the number of instructions in main is less than what we obtain using O1.
________________________________________
Optimization Levels in GCC
•	-O0: No optimization (default).
•	-O1: Basic optimization (reduces execution time while compiling quickly).
•	-O2: More aggressive optimizations.
•	-O3: Maximum optimization but increases compile time.
•	-Os: Optimizes for code size.
•	-Ofast: Highest speed optimizations (may break standard compliance).



Task 2

Factorial Code and Debugging Assembly in RISC-V
Step 1: Writing and Compiling Factorial Code on RISC-V
1.	Navigate to the Directory and Create a New C File
cd /path/to/directory
gedit factorial.c
o	Write a C program to compute the factorial of a given number.
o	Save (Ctrl + S) and close (Ctrl + W).
2.	Compile Using RISC-V GCC
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o factorial.o factorial.c
3.	View the Assembly Code
riscv64-unknown-elf-objdump -d factorial.o
________________________________________
Step 2: Debugging the Assembly Language Program (sum_1_to_n.c)
1.	Open the Objdump of the Code
riscv64-unknown-elf-objdump -d sum_1_to_n.o | less
o	This disassembles the compiled binary and allows step-by-step analysis.
o	Use /main to locate the main function.
2.	Open the Debugger in Another Terminal
spike -d pk sum_1_to_n.o
o	Spike is a RISC-V simulator used for debugging.
o	The -d flag starts the debugging mode.
3.	Set Breakpoints and Step Through Execution
o	Once inside the debugger: 
o	until pc 0xADDRESS   # Run the program until a specific instruction
o	reg                  # View register contents
o	Analyze the instruction execution 
In Task 2 of the Samsung RISC-V Talent Development Program, we extended our work by compiling and analyzing a factorial program and debugging the assembly of sum_1_to_n.c using Spike and objdump. This helped in understanding RISC-V assembly instructions and step-by-step execution for debugging.



Task 3

Identifying RISC-V Instruction Types and 32-bit Encoding
In Task 3 of the Samsung RISC-V Talent Development Program, we analyzed the assembly code obtained from the objdump of a compiled RISC-V program. We identified the instruction types and extracted their exact 32-bit binary encoding.
Key Points Covered:
1.	Understanding RISC-V
o	RISC-V is an open-source Instruction Set Architecture (ISA) based on Reduced Instruction Set Computing (RISC) principles.
o	It provides a free and flexible alternative to proprietary processor architectures.
2.	RISC-V Instruction Formats
We studied the six RISC-V instruction formats and their bit-wise structure:
o	R-type: Used for arithmetic and logical operations on registers.
o	I-type: Involves immediate values (e.g., load and arithmetic operations).
o	S-type: Used for storing data in memory.
o	B-type: Implements branching based on conditions.
o	U-type: Transfers immediate data to registers (e.g., LUI and AUIPC).
o	J-type: Handles jump instructions for function calls and loops.
3.	Task Execution
o	Identified given instructions.
o	Extracted the 32-bit binary representation of each instruction.
o	Understood how different instruction fields (opcode, func3, rs1, rs2, imm, etc.) are used in each format.
This task helped in gaining a deeper understanding of RISC-V instruction encoding and how machine-level operations are structured.




Task 4

Perform functional simulation of RISC-V instructions modeled as a Verilog netlist, observe the output waveforms using GTKWave, and analyze signal behavior for hard-coded ISA instructions.
________________________________________
Steps Completed
1. Installation of Tools
Installed required tools for Verilog simulation and waveform analysis:
sudo apt install iverilog gtkwave
2. Directory and File Setup
•	Created a new directory: 
	mkdir mnv
•	Created Verilog design and testbench files: 
	touch mnv.v mnv_tb.v
•	Implemented Verilog code for RISC-V instruction execution and testing.
3. Compilation and Simulation
•	Compiled Verilog files: 
	iverilog -o mnv_output.vvp mnv.v mnv_tb.v
•	Ran the simulation to generate the .vcd file for waveform analysis: 
	vvp mnv_output.vvp
4. Waveform Analysis
•	Opened the .vcd file in GTKWave for signal visualization: 
	gtkwave iiitb_rv32i.vcd
________________________________________
Observations
•	Hard-Coded Instructions: 
o	The design does not follow standard RISC-V encoding.
o	Instructions are hard-coded, resulting in different bit patterns than official ISA.

| Operation       |  Description                                          |   Standard ISA Encoding    |   Hard-Coded ISA Encoding   |
|-----------------|-------------------------------------------------------|----------------------------|-----------------------------|
| `ADD R6, R2, R1` | Add R2 and R1, store result in R6                     | `32'h00110333`             | `32'h02208300`             |
| `SUB R7, R1, R2` | Subtract R2 from R1, store result in R7               | `32'h402083b3`             | `32'h02209380`             |
| `AND R8, R1, R3` | Perform bitwise AND between R1 and R3, store in R8    | `32'h0030f433`             | `32'h0230a400`             |
| `OR R9, R2, R5`  | Perform bitwise OR between R2 and R5, store in R9     | `32'h005164b3`             | `32'h02513480`             |
| `XOR R10, R1, R4`| Perform bitwise XOR between R1 and R4, store in R10   | `32'h0040c533`             | `32'h0240c500`             |


•	Waveform Analysis in GTKWave: 

o	The .vcd file generated allowed detailed signal transition analysis.

o	Observed behavior of each instruction through register updates and data movement.

Waveform Analysis with GTKWave

•	Graphical signal representation helps in debugging and verifying instruction execution.

•	Critical for understanding how each instruction modifies registers and memory.

