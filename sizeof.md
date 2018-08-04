### 编译器
GCC 4.9.2 64-bit

### 基本类型
```cpp
#include <cstdio>
#include <string> 
using namespace std;
int main() {
    printf("  char: %d bytes\n", sizeof(char));
    printf("   int: %d bytes\n", sizeof(int));
    printf(" float: %d bytes\n", sizeof(float));
    printf("double: %d bytes\n", sizeof(double));
    return 0;
}
/* 输出：
  char: 1 bytes
   int: 4 bytes
 float: 4 bytes
double: 8 bytes
*/
```
### 指针
```cpp
printf("  char pointer: %d bytes\n",sizeof(char*));
printf("double pointer: %d bytes\n",sizeof(double*));
/* 输出：
  char pointer: 8 bytes
double pointer: 8 bytes
*/
```
实际上，所有pointer类型都是8bytes, 因为它们都是存放一个64位的地址
### 数组
```cpp
char c[5];
int i[5];
int ii[5][5];
printf("%d\n",sizeof(c));
printf("%d\n",sizeof(i));
printf("%d\n",sizeof(ii));
/* 输出
5
20
100
*/
```
即元素个数 x sizeof(元素类型)
### 字符串常量
```cpp
printf("%d\n",sizeof("abcd"));
/* 输出
5
/*
```
因为"abcd"类型为char[5], 注意结尾有个'\0'
### 空类
```cpp
class foo {
};
printf("%d\n",sizeof(foo));
/* 输出
1
*/
```
根据[MSDN](https://msdn.microsoft.com/en-us/library/f42z47h2.aspx)的解释，让其占一个字节而不是0的原因是，使得foo的不同对象有不同的地址，才能比较某两个pointer指向的东西是否是一个对象。
### 类
```cpp
class foo1{
	int a;
};
class foo2 {
	int a;
	int b;
	string c;
};
class foo3 {
	int a;
	string b;
	int c;
};
int main() {
	printf("%d\n",sizeof(foo1));
	printf("%d\n",sizeof(foo2));
	printf("%d\n",sizeof(foo3));
	return 0;
}
/* 输出：
4
16
24
*/
```
注意foo2和foo3, 它们定义成员变量的顺序导致了它们size不同！原因是编译器做了对齐。见[stackoverflow](https://stackoverflow.com/questions/14510711/how-is-the-size-of-a-c-class-determined)
### 带成员函数的类
[stackoverflow](https://stackoverflow.com/questions/6552319/c-sizeof-of-a-class-with-functions):
>Member functions aren't physically "inside" a class, they're really just free functions with a hidden argument and a namespace and access control
### 带static成员的类
```cpp
class foo {
	static int a;
};
int foo::a = 5;

int main() {
    printf("%d\n",sizeof(foo));
    return 0;
}
/* 输出
1
/*
```
static成员不影响, 应该也只是类似与前面成员函数的access control
### 带虚函数的类
```cpp
class foo {
    virtual void f1();
};
class bar {
    virtual void f2();
};
class child: foo, bar {
};
int main() {
    printf("%d\n",sizeof(foo));
    printf("%d\n",sizeof(child));
    return 0;
}
/* 输出
8
16
*/
```
foo多了个vptr，child多了两个vptr
### std::string
```cpp
printf("%d\n",sizeof(std::string));
/* 输出
8
*/
```
与不同编译器对string的实现有很大关系，见[cnblogs](https://www.cnblogs.com/tntboom/p/4550271.html)
### 其它
[知乎](https://www.zhihu.com/question/26090484)
>sizeof 这个编译时函数的目的是得到一个变量或类型占用的字节数，它的求值是由编译器完成时，没有运行时逻辑
