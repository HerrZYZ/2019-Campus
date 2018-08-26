## Static Lib
Reference: [GeeksForGeeks](https://www.geeksforgeeks.org/static-vs-dynamic-libraries/)

c code:
```cpp
// libfoo.h
void foo();

// libfoo.c
#include "libfoo.h"
int main(int argc, char const *argv[]) {
    foo();
    return 0;
}

// main.c
#include <stdio.h>
void foo() {
    printf("foo() called from a static library.\n");
}
```
shell command:
```
gcc -c libfoo.c -o libfoo.o
ar rcs libfoo.a libfoo.o

gcc -c main.c -o main.o
gcc -o main main.o -L . -l foo
./main
```
run
```
size main
```
to get size:
```
text    data     bss     dec     hex filename
1598     600       8    2206     89e main
```

### Dynamic Lib
Reference: [cprogramming](https://www.cprogramming.com/tutorial/shared-libraries-linux-gcc.html)

```
gcc -c -Wall -Werror -fpic libfoo.c
gcc -shared -o libfoo.so libfoo.o
gcc -L . -o main main.c -l foo
export LD_LIBRARY_PATH=your path to libfoo.so
```
run
```
size main
```
```
 text    data     bss     dec     hex filename
 1705     616       8    2329     919 main
```
It's bigger than static version, why?
