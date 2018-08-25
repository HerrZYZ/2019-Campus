
c++ async的解释参考[这里](https://www.cnblogs.com/qicosmos/p/3534211.html)

```cpp
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
输出
```
Main thread id: 1
Thread id: 2
Async call
Main end.
```
