### 虚函数表Basic
[CSDN](https://blog.csdn.net/haoel/article/details/1948051/)

### Q & A
#虚函数表是针对类的还是针对对象的?

类。显然没必要为同一个类的每个对象都保存一份虚函数表，每个对象都有一个指针指向那个class-specific的虚函数表就足矣。

#什么时候该使用虚析构器？

[Stackoverflow](https://stackoverflow.com/questions/461203/when-to-use-virtual-destructors)

>if the static type of the object to be deleted is different from its dynamic type, the static type shall be a base class of the dynamic type of the object to be deleted and the static type shall have a virtual destructor or the behavior is undefined.

eg:
```cpp
class Base {
    // some virtual methods
    // destructor should be virtual!
};

class Derived : public Base {
    ~Derived() {
        // Do some important cleanup
    }
};
Base *b = new Derived();
// use b
delete b; // Here's the problem!, that's why destructor should be virtual!
```

### How virtual function's are called?
```cpp
#include <cstdio>

class Animal {
public:
    virtual void _666() {
        printf("666");
    }
    virtual void _wow() {
        printf("wow");
    }
    ~Animal(){};
};

int _2333(int dummy, Animal* animal) {
    dummy++;
    animal->_666();
    animal->_wow();
    return dummy;
}
```
asm:
```asm
	.file	"virtial.cpp"
	.intel_syntax noprefix
	.text
	.globl	_Z5_2333iP6Animal
	.type	_Z5_2333iP6Animal, @function
_Z5_2333iP6Animal:
.LFB5:
	.cfi_startproc
	push	rbp
	.cfi_def_cfa_offset 16
	.cfi_offset 6, -16
	mov	rbp, rsp
	.cfi_def_cfa_register 6
	sub	rsp, 16
	mov	DWORD PTR -4[rbp], edi  # rbp~rbp-4 is dummy
	mov	QWORD PTR -16[rbp], rsi # rbp-8~rbp-16 is animal pointer
	add	DWORD PTR -4[rbp], 1 # add dummy
	mov	rax, QWORD PTR -16[rbp] # rax's value = animial address
	mov	rax, QWORD PTR [rax] # rax's value = vptr's value(i.e. vtable's addr)
	mov	rax, QWORD PTR [rax] # rax's value = first virtual fun's address
	mov	rdx, QWORD PTR -16[rbp] 
	mov	rdi, rdx
	call	rax  # call _666
	mov	rax, QWORD PTR -16[rbp] # rax's value = animial address
	mov	rax, QWORD PTR [rax] # rax's value = vptr's value
	add	rax, 8  # rax's value = vtable's address + 8
	mov	rax, QWORD PTR [rax] # rax's value = second virtual fun's address
	mov	rdx, QWORD PTR -16[rbp]
	mov	rdi, rdx
	call	rax # call second virtual fun
	mov	eax, DWORD PTR -4[rbp]
	leave
	.cfi_def_cfa 7, 8
	ret
	.cfi_endproc
.LFE5:
	.size	_Z5_2333iP6Animal, .-_Z5_2333iP6Animal
	.ident	"GCC: (Ubuntu 7.3.0-16ubuntu3) 7.3.0"
	.section	.note.GNU-stack,"",@progbits

```
