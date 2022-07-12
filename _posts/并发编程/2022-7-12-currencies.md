---
title: C++并发编程 (1) thread、join、lambda
date: 2022-7-12
tag: [C++, 并发编程]
---
- ### thread
C++11提供了``线程库``包含在`thread.h`头文件内，这里用多线程技术演示经典程序`hello world`如下：
```cpp
#include <iostream>
#include <thread.h>

void foo () {
    std::cout << "hello world" <<'\n';
}

int main () {
    std::thread t1(foo);
    t1.join();
    return 0;
}
```
这里需要注意:

- 当`thread`接受一个函数指针实例化出`t1`时，线程开始启动执行
- 没有执行`join`函数时，`t1`**线程**有可能未执行到输出语句，`main`**主进程**便执行到了`return 0;`正常**退出**，`t1`被回收销毁
- 在Linux平台上编译上述代码时，由于历史原因，线程链接库并不处于标准链接库中，需要编译时加入链接指令`-l pthread`