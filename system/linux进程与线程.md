[cnblogs](https://www.cnblogs.com/jingzhishen/p/4433023.html)
#### 用户级线程
线程管理工作由应用程序完成，内核意识不到线程的存在。比如一个进程由10个线程，但在内核看来，这就是1个进程而已，该进程任一个线程阻qi塞都会导致该进程挂起，并且无法利用多处理器技术。
用户级线程的优点是线程切换不用内核态和用户态的转换。

#### 内核级线程
线程管理由内核完成，进程的一个线程被阻塞，该进程的其它线程仍然可以被内核调度。

#### 轻量级进程
>a LWP runs in user space on top of a single kernel thread and shares its address space and system resources with other LWPs within the same process
