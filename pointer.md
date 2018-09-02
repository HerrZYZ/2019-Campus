#### 一. 智能指针是怎么实现的？什么时候改变引用计数？

1. 构造函数中计数初始化为1；
2. 拷贝构造函数中计数值加1；
3. 赋值运算符中，左边的对象引用计数减一，右边的对象引用计数加一；
4. 析构函数中引用计数减一；
5. 在赋值运算符和析构函数中，如果减一后为0，则调用delete释放对象.

from [知乎](https://www.zhihu.com/question/34574154/answer/253165162)

#### 二. 指针常量 vs 常量指针
[知乎](https://www.zhihu.com/question/37608201)
```cpp
#include <cstdio>
int main() {
    int a = 1;
    int b = 2;
    int* p1 = &a;
    const int* p2 = &a;
    int* const p3 = &a;
    *p1 = 1; //OK
    p1 = &b; //OK

    *p2 = 2; //not OK
    p2 = &b; //OK

    *p3 = 2; //OK
    p3 = &b; //not OK
}
```
#### 三. 引用怎么实现的？
[Stackoverflow](https://stackoverflow.com/questions/3954764/how-is-reference-implemented-internally)
>The natural implementation of a reference is indeed a pointer. However, do not depend on this in your code
```cpp
int int_int_bss; //in bss section, 4 bytes
int& p = int_int_bss; //p in data section, 8 bytes
```
```
text    data     bss     dec     hex filename
0       8       4      12       c reference.o
```

#### 四. 为何能从函数返回unique_ptr？
>unique_ptr<T> does not allow copy construction, instead it supports move semantics. Yet, I can return a unique_ptr<T> from a function and assign the returned value to a variable. why?
    
[Stackoverflow](https://stackoverflow.com/questions/4316727/returning-unique-ptr-from-functions)
