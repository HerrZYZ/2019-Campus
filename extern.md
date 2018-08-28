### 声明 VS 定义(Declaration VS Definition)
```c
//declare.c
//only Declaration
void foo(int a, int b);
```
```
gcc -s declare.c -o declare.s
```
汇编文件中没有任何关于foo的东西。
```asm
.file	"declare.c"
.text
.ident	"GCC: (Ubuntu 7.3.0-16ubuntu3) 7.3.0"
.section	.note.GNU-stack,"",@progbits
```
```c
//Definition
void foo(int a, int b) {}
```
汇编文件中会有函数foo。foo的代码也会出现在obj文件中.text Section， 并且foo出现在.symtab

### 只声明而不定义变量
```cpp
//declare.h
#ifndef something
#define something
int var = 23333;
#endif
```
```cpp
//delcare.c
#include "declare.h"
#include <stdio.h>
int main(int argc, char const *argv[]) {
    printf("%d\n", var);
    return 0;
}
// g++ -declare.c -o declare
// ok

//delcare.c
#include "declare.h"
#include <stdio.h>
extern int var;
int main(int argc, char const *argv[]) {
    printf("%d\n", var);
    return 0;
}
// g++ -declare.c -o declare
// ok

//declare.c
#include <stdio.h>
int main(int argc, char const *argv[]) {
    printf("%d\n", var);
    return 0;
}
// g++ -c -declare.c -o declare.o
// not ok

//declare.c
#include <stdio.h>
extern int var;
int main(int argc, char const *argv[]) {
    printf("%d\n", var);
    return 0;
}
// g++ -c -declare.c -o declare.o
// ok
```
