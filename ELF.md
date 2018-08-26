### C Code
```cpp
#include <unistd.h> 
#include <string.h> 

int init0_var = 0;
int init_var = 1;

void a_fun(char *s) { 
    write(1, s, strlen(s)); 
}
```
```
gcc -c a.c -o a.o
```
### Analyze a.o 
Reference 

1. [Wikipedia ELF](https://en.wikipedia.org/wiki/Executable_and_Linkable_Format)
2. [ELF Format](http://www.skyfree.org/linux/references/ELF_Format.pdf)
#### ELF Header

![ELF Header](https://github.com/PanJianning/CPP-Basic-Question/blob/master/pictures/elf_header.PNG)

Run: 
```
readelf a.o -h 
```
Result:
```
ELF Header:
  Magic:   7f 45 4c 46 02 01 01 00 00 00 00 00 00 00 00 00
  Class:                             ELF64
  Data:                              2's complement, little endian
  Version:                           1 (current)
  OS/ABI:                            UNIX - System V
  ABI Version:                       0
  Type:                              REL (Relocatable file)
  Machine:                           Advanced Micro Devices X86-64
  Version:                           0x1
  Entry point address:               0x0
  Start of program headers:          0 (bytes into file)
  Start of section headers:          792 (bytes into file)
  Flags:                             0x0
  Size of this header:               64 (bytes)
  Size of program headers:           0 (bytes)
  Number of program headers:         0
  Size of section headers:           64 (bytes)
  Number of section headers:         12
  Section header string table index: 11
```
There is no program headers in a.o, offset of section headers is 792 bytes

### Section headers
Go to offset 792

By convention, the first section header is all zero:

![zero section](https://github.com/PanJianning/CPP-Basic-Question/blob/master/pictures/zero_section.PNG)

The second section header:

![text section](https://github.com/PanJianning/CPP-Basic-Question/blob/master/pictures/text%20section.PNG)

According to [WikiPedia](https://en.wikipedia.org/wiki/Executable_and_Linkable_Format), break it into some field：

![](https://github.com/PanJianning/CPP-Basic-Question/blob/master/pictures/modified_text%20section.png)

Actually, this is the .text section.

Run the following command
```
readelf a.o -S
```
We would know that there 12 section headers in total.
```
There are 12 section headers, starting at offset 0x318:

Section Headers:
  [Nr] Name              Type             Address           Offset
       Size              EntSize          Flags  Link  Info  Align
  [ 0]                   NULL             0000000000000000  00000000
       0000000000000000  0000000000000000           0     0     0
  [ 1] .text             PROGBITS         0000000000000000  00000040
       000000000000002f  0000000000000000  AX       0     0     1
  [ 2] .rela.text        RELA             0000000000000000  00000270
       0000000000000030  0000000000000018   I       9     1     8
  [ 3] .data             PROGBITS         0000000000000000  00000070
       0000000000000004  0000000000000000  WA       0     0     4
  [ 4] .bss              NOBITS           0000000000000000  00000074
       0000000000000004  0000000000000000  WA       0     0     4
  [ 5] .comment          PROGBITS         0000000000000000  00000074
       0000000000000025  0000000000000001  MS       0     0     1
  [ 6] .note.GNU-stack   PROGBITS         0000000000000000  00000099
       0000000000000000  0000000000000000           0     0     1
  [ 7] .eh_frame         PROGBITS         0000000000000000  000000a0
       0000000000000038  0000000000000000   A       0     0     8
  [ 8] .rela.eh_frame    RELA             0000000000000000  000002a0
       0000000000000018  0000000000000018   I       9     7     8
  [ 9] .symtab           SYMTAB           0000000000000000  000000d8
       0000000000000150  0000000000000018          10     8     8
  [10] .strtab           STRTAB           0000000000000000  00000228
       0000000000000041  0000000000000000           0     0     1
  [11] .shstrtab         STRTAB           0000000000000000  000002b8
       0000000000000059  0000000000000000           0     0     1
Key to Flags:
  W (write), A (alloc), X (execute), M (merge), S (strings), I (info),
  L (link order), O (extra OS processing required), G (group), T (TLS),
  C (compressed), x (unknown), o (OS specific), E (exclude),
  l (large), p (processor specific)
```
### Sections
From section headers, we konw that 
####.text section is at offset 0x40
![text section](https://github.com/PanJianning/CPP-Basic-Question/blob/master/pictures/text.PNG)
#### .data section at 0x70
![data section](https://github.com/PanJianning/CPP-Basic-Question/blob/master/pictures/data.PNG)
#### .bss section at 0x74
Actually, bss section does not occupy any space here, the loader only need to know bss section's size from section headers, and zero out a space for it.
#### .comment section at 0x74
![comment section](https://github.com/PanJianning/CPP-Basic-Question/blob/master/pictures/strtab.PNG)
#### .strtab section at 0x228
![strtab section](https://github.com/PanJianning/CPP-Basic-Question/blob/master/pictures/strtab.PNG)

Run 
```
readelf a.o -p .strtab
```
to see .strtab section's content:
```
String dump of section '.strtab':
  [     1]  a.c
  [     5]  init0_var
  [     f]  init_var
  [    18]  a_fun
  [    1e]  _GLOBAL_OFFSET_TABLE_
  [    34]  strlen
  [    3b]  write
```
#### .shstrtab section at 0x2b8
![shstrtab section](https://github.com/PanJianning/CPP-Basic-Question/blob/master/pictures/shstrtab.PNG)
