### 什么时候使用全局静态变量？
Reference: [Stackoverflow](https://stackoverflow.com/questions/1856599/when-to-use-static-keyword-before-global-variables)
```cpp
//foo.cpp
int a = 1;

//bar.cpp
int a = 2;

//main.cpp
int main() {
  return 0;
}
```
compile and link
```
g++ -c foo.cpp -o foo.o
g++ -c bar.cpp -o bar.o
g++ main.cpp -o main far.o bar.o
```
Failed
```
header2.o:(.data+0x0): multiple definition of `a'
header1.o:(.data+0x0): first defined here
collect2: error: ld returned 1 exit status
```
Change def. of a to static will solve the problem.
```cpp
//foo.cpp
static int a = 1;

//bar.cpp
static int a = 2;

//main.cpp
int main() {
  return 0;
}
```
