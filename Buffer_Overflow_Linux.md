# Buffer overflow notes:
- Buffer overflow basically requires you to stack memory or elements of the stack through a loophole in a program.
- Suppose too much data is written in the buffer and it is not limited by the program then certain specific registers might also be overwritten which allow code to be executed.
- An exploit is a code that causes the service to perform an operation we want by abusing the found vulnerability. Such codes often serve as proof-of-concept (POC) in our reports.



## Von Neumann Architecture: 
- 4 functional units :
                          **Memory
                          Control Unit
                          Arithmetical Logical Unit
                          Input/Output Unit**

- The aritmetical logical unit and control unit are combined in the actual Cpu.
-  The instructions are executed one after the other, step by step. The commands and data are fetched from memory by the CU

-  The connection between processor, memory, and input/output unit is called a bus system, which is not mentioned in the original Von-Neumann architecture but plays an essential role in practice. In the Von-Neumann architecture, all instructions and data are transferred via the bus system.


### Memory: 

- Primary Memory:
        -Internal memory like cache and ram
- Secondary Memory:
        - External Memory like hdd,ssd.

#### CU : 
-The CU contains the Instruction Register (IR), which contains all instructions that the processor decodes and executes accordingly.The data used during execution is temporarily stored in registers.

- CPU architectures is built in a specific way, called Instruction Set Architecture (ISA), which the CPU uses to execute its processes.
- Types of IAS:
        **CISC - Complex Instruction Set Computing
        RISC - Reduced Instruction Set Computing
        VLIW - Very Long Instruction Word
        EPIC - Explicitly Parallel Instruction Computing**

-Instruction Cycle
![instructiom](https://github.com/user-attachments/assets/ec2bbd27-8591-47c3-b5d9-ce71634677e4)




