# Stack-Based Buffer Overflow

- Buffer overflows are errors that allow data that is too large to fit into a buffer of the operating system's memory that is not large enough, thereby overflowing this buffer
- As a result of this mishandling, the memory of other functions of the executed program is overwritten, potentially creating a security vulnerability.

- Such a program (binary file), is a general executable file stored on a data storage medium. There are several different file formats for such executable binary files. For example, the Portable Executable Format (PE) is used on Microsoft platforms.
- Another format for executable files is the Executable and Linking Format (ELF), supported by almost all modern UNIX variants


## Memory Structure: 

![buffer_overflow_1](https://github.com/user-attachments/assets/eb1c5086-9b69-4cfe-a785-8f001e0b9b37)

- .text
The .text section contains the actual assembler instructions of the program. This area can be read-only to prevent the process from accidentally modifying its instructions. Any attempt to write to this area will inevitably result in a segmentation fault.

-.data
The .data section contains global and static variables that are explicitly initialized by the program.

-.bss
Several compilers and linkers use the .bss section as part of the data segment, which contains statically allocated variables represented exclusively by 0 bits.


- The Heap
Heap memory is allocated from this area. This area starts at the end of the ".bss" segment and grows to the higher memory addresses.

-Stack memory is a Last-In-First-Out data structure in which the return addresses, parameters, and, depending on the compiler options, frame pointers are stored.


### Practical: 

-bow.c a vuln app with strcpy func.
```c
#include <stdlib.h>
#include <stdio.h>
#include <string.h>

int bowfunc(char *string) {

	char buffer[1024];
	strcpy(buffer, string);
	return 1;
}

int main(int argc, char *argv[]) {

	bowfunc(argv[1]);
	printf("Done.\n");
	return 1;
}
```
- using gdb to decompile in assembly :
```
student@nix-bow:~$ gdb -q bow32

Reading symbols from bow...(no debugging symbols found)...done.
(gdb) disassemble main

Dump of assembler code for function main:
   0x00000582 <+0>: 	lea    0x4(%esp),%ecx
   0x00000586 <+4>: 	and    $0xfffffff0,%esp
   0x00000589 <+7>: 	pushl  -0x4(%ecx)
   0x0000058c <+10>:	push   %ebp
   0x0000058d <+11>:	mov    %esp,%ebp
   0x0000058f <+13>:	push   %ebx
   0x00000590 <+14>:	push   %ecx
   0x00000591 <+15>:	call   0x450 <__x86.get_pc_thunk.bx>
   0x00000596 <+20>:	add    $0x1a3e,%ebx
   0x0000059c <+26>:	mov    %ecx,%eax
   0x0000059e <+28>:	mov    0x4(%eax),%eax
   0x000005a1 <+31>:	add    $0x4,%eax
   0x000005a4 <+34>:	mov    (%eax),%eax
   0x000005a6 <+36>:	sub    $0xc,%esp
   0x000005a9 <+39>:	push   %eax
   0x000005aa <+40>:	call   0x54d <bowfunc>
   0x000005af <+45>:	add    $0x10,%esp
   0x000005b2 <+48>:	sub    $0xc,%esp
   0x000005b5 <+51>:	lea    -0x1974(%ebx),%eax
   0x000005bb <+57>:	push   %eax
   0x000005bc <+58>:	call   0x3e0 <puts@plt>
   0x000005c1 <+63>:	add    $0x10,%esp
   0x000005c4 <+66>:	mov    $0x1,%eax
   0x000005c9 <+71>:	lea    -0x8(%ebp),%esp
   0x000005cc <+74>:	pop    %ecx
   0x000005cd <+75>:	pop    %ebx
   0x000005ce <+76>:	pop    %ebp
   0x000005cf <+77>:	lea    -0x4(%ecx),%esp
   0x000005d2 <+80>:	ret 
```

-
