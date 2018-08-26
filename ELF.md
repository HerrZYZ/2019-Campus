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

