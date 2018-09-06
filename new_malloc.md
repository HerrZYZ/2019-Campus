[cnblog](https://www.cnblogs.com/QG-whz/p/5060894.html)
### Free Store vs Heap
>从技术上来说，堆（heap）是C语言和操作系统的术语。堆是操作系统所维护的一块特殊内存，它提供了动态分配的功能，当运行程序调用malloc()时就会从中分配，
稍后调用free可把内存交还。而自由存储是C++中通过new和delete动态分配和释放对象的抽象概念，通过new来申请的内存区域可称为自由存储区。基本上，
所有的C++编译器默认使用堆来实现自由存储，也即是缺省的全局运算符new和delete也许会按照malloc和free的方式来被实现，这时藉由new运算符分配的对象，
说它在堆上也对，说它在自由存储区上也正确。但程序员也可以通过重载操作符，改用其他内存来实现自由存储，例如全局变量做的对象池，
这时自由存储区就区别于堆了。

### new vs malloc
[stackoverflow](https://stackoverflow.com/questions/240212/what-is-the-difference-between-new-delete-and-malloc-free#240308)
