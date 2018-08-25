### Reference
[memory-layout-of-c-program](https://www.geeksforgeeks.org/memory-layout-of-c-program/)

### Experiments on Win10
一. 初始
```cpp
// mem_layout.c
#include <stdio.h>
int main() {
    return 0;
}
```
```shell
gcc mem_layout.c -o mem_layout.exe
size mem_layout.exe
```
结果
```cpp
text    data     bss     dec     hex filename
10284    2316    2656   15256    3b98 mem_layout.exe
```
dec和hex分别表示总大小的十进制表示和十六进制表示，Never mind.

二. 添加未初始化全局变量
```cpp
#include <stdio.h>
int uninit_global_var;
int main() {
    return 0;
}
```
结果
```cpp
 text    data     bss     dec     hex filename
10284    2316    2672   15272    3ba8 mem_layout.exe
```
bss多了16字节，16字节而非4字节应该是对齐的结果？

三. 添加初始化全局变量(不为0)
```cpp
#include <stdio.h>
int init_global_var = 1;
int main() {
    return 0;
}
```
结果
```
 text    data     bss     dec     hex filename
10284    2332    2656   15272    3ba8 mem_layout.exe
```
data多了16字节

四. 静态
...
