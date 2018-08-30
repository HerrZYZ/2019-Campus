### Variable in Stack
```cpp
#include <cstdio>
void foo() {
    int a = 233333333;
    int b = 666666666;
    printf("%d\n", a);
}
```
check Section size:
```
 g++ -c reference.cpp -o reference.o
 size reference.o
```
```
text    data     bss     dec     hex filename
77       0       0      77      4d reference.o
```
check assemble file
```
g++ -S reference.cpp -o reference.s -masm=intel
```
```asm
	.file	"reference.cpp"
	.intel_syntax noprefix
	.text
	.section	.rodata
.LC0:
	.string	"%d\n"
	.text
	.globl	_Z3foov
	.type	_Z3foov, @function
_Z3foov:
.LFB0:
	.cfi_startproc
	push	rbp
	.cfi_def_cfa_offset 16
	.cfi_offset 6, -16
	mov	rbp, rsp
	.cfi_def_cfa_register 6
	sub	rsp, 16
	mov	DWORD PTR -8[rbp], 233333333  # a = 233333333
	mov	DWORD PTR -4[rbp], 666666666 # b = 666666666
	mov	eax, DWORD PTR -8[rbp] # move a to eax for printf
	mov	esi, eax
	lea	rdi, .LC0[rip]
	mov	eax, 0
	call	printf@PLT
	nop
	leave
	.cfi_def_cfa 7, 8
	ret
	.cfi_endproc
.LFE0:
	.size	_Z3foov, .-_Z3foov
	.ident	"GCC: (Ubuntu 7.3.0-16ubuntu3) 7.3.0"
	.section	.note.GNU-stack,"",@progbits

```
