#### 一. 智能指针是怎么实现的？什么时候改变引用计数？

1. 构造函数中计数初始化为1；
2. 拷贝构造函数中计数值加1；
3. 赋值运算符中，左边的对象引用计数减一，右边的对象引用计数加一；
4. 析构函数中引用计数减一；
5. 在赋值运算符和析构函数中，如果减一后为0，则调用delete释放对象.

from [知乎](https://www.zhihu.com/question/34574154/answer/253165162)

#### 二. 指针 VS 引用
[知乎](https://www.zhihu.com/question/37608201)
```cpp
int num = 1;
const int* p_num1 = a;
int* const p_num2 = a;
```
引用怎么实现的？
[Stackoverflow](https://stackoverflow.com/questions/3954764/how-is-reference-implemented-internally)
>The natural implementation of a reference is indeed a pointer. However, do not depend on this in your code
