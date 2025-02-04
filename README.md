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
