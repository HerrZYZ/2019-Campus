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
