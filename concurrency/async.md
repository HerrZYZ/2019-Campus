
c++ async的解释参考[这里](https://www.cnblogs.com/qicosmos/p/3534211.html)

以下代码在Win10 Ubuntu子系统下测试

```cpp
// test1.cpp
#include <future>
#include <iostream>
#include <chrono>

void fun() {
    std::cout << "Thread id: " << std::this_thread::get_id() << std::endl;
    std::cout << "Async call" << std::endl;
}

int main(int argc, char const *argv[]) {
    using namespace std::chrono_literals; // C++14
    std::cout << "Main thread id: " << std::this_thread::get_id() << std::endl;
    std::future<void> result(std::async(std::launch::async, fun));
    std::this_thread::sleep_for(1s);
    std::cout << "Main end." << std::endl;
    result.get();
    return 0;
}
```
compile, run
```
g++ test1.cpp -std=c++14 -pthread
./a.out
```
outputs
```
Main thread id: 139843056305984
Thread id: 139843036776192
Async call
Main end.
```

>在成员函数函数上用async
```cpp
#include <future>
#include <iostream>
#include <functional>

class Foo {
public:
    int sum(int a, int b) {
        return a+b;
    }
private:
    int a;
};

int main(int argc, char const *argv[]) {
    Foo foo;
    std::future<int> result(std::async(std::launch::async, &Foo::sum, &foo, 2, 3));
    std::cout << "Message from main." << std::endl;
    std::cout << result.get() << std::endl;
    return 0;
}
```
